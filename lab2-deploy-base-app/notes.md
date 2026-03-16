# Lab 2: Bedrock AI Integration & EC2 Deployment – TravelGuideAI

## ✅ Objective

- Update the TravelGuideAI Flask application to add generative AI features using Amazon Bedrock.
- Create an Amazon Bedrock knowledge base using an S3 data source and OpenSearch Serverless vector store.
- Test retrieval-augmented generation (RAG) in the Bedrock console and in the application UI.
- Package the application and deploy it to an Amazon EC2 instance using userdata, systemd, and NGINX.
- Verify successful AI response generation in both local and EC2-hosted environments.

---

## Task 1: Add Amazon Bedrock AI Features to the Application

- Integrated Amazon Bedrock for AI-based itinerary and review responses.
- Extracted the provided application update:
  ```bash
  unzip -o ~/update.zip
  ```
- Key file changes:
  - `app.py` – Added routes for Bedrock AI: streaming text generation (`invoke_model_with_response_stream`) - `/generate`, knowledge base retrieval + generation (`retrieve_and_generate`) - `/knowledge`
  - `test_app.py` – Updated tests to mock Bedrock calls and validate AI endpoints
  - `templates/city.html` – UI updates for: 🧭 Itinerary Planner + 💬 Review Bot
  - `scripts/dbb_reviews_to_s3.py` – Exports DynamoDB reviews into S3 objects + metadata files for filtering
  - `deployment/userdata.sh` – (bootstraps EC2: Python env, app install, systemd service, NGINX)
  - `deployment/travelapp.service` – (systemd unit config)
  - `deployment/travelapp.conf` – (NGINX reverse proxy configuration)

📸 `update-unzip-output.png`, `source-control-diff.png`

### Test Bedrock AI Update

- Ran build script:
```bash
  ./local_build.sh
```
- Confirmed:
  - ✅ PyLint: 10/10
  - ⚠️ Code coverage: 81% - Due to some incomplete test cases.
  - Verified that all 6 updated tests pass

📸 `local-build-success.png`, `coverage-report.png`

---

## Task 2: Create Amazon Bedrock Knowledge Base Resources

### Populate S3 data source from DynamoDB reviews 

- Ran the script to export reviews to the knowledge base S3 bucket:
```bash
  python3 scripts/dbb_reviews_to_s3.py
```
- Verified that each review produces:
  - a `.txt` object (review content)
  - a `.metadata.json` object (metadata used by knowledge base results)

### Create Bedrock Knowledge Base (Vector Store)

- Created knowledge base: `travel-kb`
- Selected:
  - Existing service role: `AmazonBedrockExecutionRoleForKnowledgeBase`
  - Data source: S3 bucket starting with `knowledge-base-bucket...`
  - Embeddings model: Titan Text Embeddings V2
  - Vector store type: OpenSearch Serverless (existing collection)
  - Used lab-provided `CollectionARN`
- Synced the data source and waited for status: ✅ Available

📸 `s3-populated-files.png`, `s3-reviews-uploaded.png`, `bedrock-kb-create-1-details.png`, `bedrock-kb-create-2-embedding-vectorstore.png`, `bedrock-kb-sync-status.png`

### Test Knowledge Base in Bedrock Console

- Used “Test knowledge base”
- Selected model: Nova Lite (On demand)
- Ran prompt: “What should I do in Tokyo?”
- Bedrock responded using RAG + metadata references
- Opened “Details” to confirm retrieved chunks + metadata were included

📸 `bedrock-kb-test-nova-lite.png`, `bedrock-kb-test-details-metadata.png`

### Run the AI-Enhanced Application Locally

- Exported knowledge base ID for the application:
```bash
  export KNOWLEDGE_BASE_ID=`aws bedrock-agent list-knowledge-bases \
    --query "knowledgeBaseSummaries[0].knowledgeBaseId" \
    --output text`
```
- Launched the app locally: `flask run`
- Verified New UI features: 🧭 Itinerary Planner (text generation) + 💬 Review Bot (RAG from knowledge base)

📸 `kb-id-export-command.png`, `local-ai-ui-itinerary-reviewbot.png`, `flask-run-local.png`

---

## Task 3: Deploy the Updated Application to EC2

### Package and upload deployment artifact

- Created application archive from Git:
```bash
  git archive -o /tmp/app.zip HEAD
```
- Uploaded app.zip to S3 via `$DEPLOYMENT_BUCKET`
```bash
  aws s3 cp /tmp/app.zip s3://$DEPLOYMENT_BUCKET
```
- Launched EC2 instance using `userdata.sh` to auto-install app, systemd, and NGINX
```bash
  aws ec2 run-instances \
    --image-id $AMI_ID \
    --instance-type t2.micro \
    --subnet-id $SUBNET_ID \
    --security-group-ids $SECURITY_GROUP_ID \
    --associate-public-ip-address \
    --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=webserver}]' \
    --iam-instance-profile Name=TravelApplicationInstanceProfile \
    --user-data file:///home/ec2-user/environment/deployment/userdata.sh
```

📸 `app-zip-archive.png`, `s3-upload-appzip.png`, `ec2-run-instances-output.png`

### Verify EC2 Deployment

- Retrieved EC2 public IP
 ```bash
  IP_ADDRESS=`aws ec2 describe-instances \
    --filters "Name=tag:Name,Values=webserver" \
    --query "Reservations[].Instances[].PublicIpAddress" \
    --output text`
  echo $IP_ADDRESS
```
- Opened http://<PublicIP> in browser
- Waited a few minutes for bootstrap; refreshed until city list loaded
- Verified Bedrock features working (Itinerary Planner + Review Bot)

📸 `ec2-public-ip-output.png`, `ec2-deployed-app-browser.png`

## ✅ Summary
Successfully:
- Added Bedrock-powered text generation + knowledge base Q&A features to the Flask app
- Built a knowledge base using S3 + OpenSearch Serverless with Titan embeddings
- Tested RAG responses in Bedrock console using Nova Lite
- Ran the AI-enhanced app locally and validated new UI features
- Deployed the application to EC2 using userdata, systemd, and NGINX