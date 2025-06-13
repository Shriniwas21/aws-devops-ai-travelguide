# Lab 2: Bedrock AI Integration & EC2 Deployment – TravelGuideAI

## ✅ Objective

- Integrate Generative AI features into an existing Flask-based travel app using Amazon Bedrock.
- Populate a knowledge base with travel review data stored in DynamoDB, pushed to S3.
- Enable Titan foundation models and configure Bedrock with OpenSearch Serverless for RAG.
- Launch and test AI-enhanced app locally using Bedrock API.
- Package the application and deploy it to an Amazon EC2 instance using userdata, systemd, and NGINX.
- Verify successful AI response generation in both local and EC2-hosted environments.

---

## Task 1: Add Amazon Bedrock AI Features

- Integrated Amazon Bedrock for AI-based itinerary and review responses.
- Key file changes:
  - `app.py` – Added routes for Bedrock AI: `/generate`, `/knowledge`
  - `test_app.py` – Added unit tests for new AI features (mocked Bedrock APIs)
  - `templates/city.html` – Added UI for Itinerary Planner + Review Bot
  - `scripts/dbb_reviews_to_s3.py` – Script to extract DynamoDB reviews into S3
  - `deployment/userdata.sh` – EC2 install + setup script
  - `deployment/travelapp.service` – Systemd unit config
  - `deployment/travelapp.conf` – NGINX reverse proxy config

📸 `source-control-changes.png`, `terminal-unzip-output.png`

### Test Bedrock AI Update

- Ran build script:
```bash
  ./local_build.sh
```
- ✅ PyLint: 10/10
- ✅ Code coverage: 100%
- Verified that all 6 updated tests pass

📸 `pylint-after-bedrock-update.png`, `coverage-after-bedrock-update.png`

---

## Task 2: Create Bedrock Knowledge Base

- Populated S3 with review content + metadata for RAG
```bash
  python3 scripts/dbb_reviews_to_s3.py
```
- Enabled Titan Text G1 + Embedding V2 models
- Created knowledge base using OpenSearch Serverless
- Synced vector store successfully: ✅ Available

📸 `s3-populated-files.png`, `bedrock-model-access.png`, `bedrock-kb-config.png`, `bedrock-sync-complete.png`

### Test KB in Bedrock Console

- Ran prompt: “What should I do in Tokyo?”
- Bedrock responded using RAG + metadata references
- Verified metadata chunks and source document traceability

📸 `bedrock-kb-test-response.png`

### Local AI App Launch

- Exported Bedrock KB ID:
 ```bash
  export KNOWLEDGE_BASE_ID=`aws bedrock-agent list-knowledge-bases --query "knowledgeBaseSummaries[0].knowledgeBaseId" --output text`
  flask run
```
- Launched AI-enhanced app on `localhost:5000`
- Verified New features: 🧭 Itinerary Planner + 💬 Review Bot

📸 `ai-app-local-ui.png`, `terminal-flask-ai.png`

---

## Task 3: Package + Deploy App to EC2

- Archived entire app + deployment config
- Uploaded app.zip to S3 via `$DEPLOYMENT_BUCKET`
 ```bash
  git archive -o /tmp/app.zip HEAD
  aws s3 cp /tmp/app.zip s3://$DEPLOYMENT_BUCKET
```
- Launched EC2 instance using `userdata.sh` to auto-install app, systemd, and NGINX
 ```bash
  aws ec2 run-instances ... --user-data file://deployment/userdata.sh
```

📸 `s3-upload-appzip.png`, `ec2-run-output.png`

### Verify EC2 Deployment

- Retrieved EC2 public IP and accessed deployed app via browser
 ```bash
  aws ec2 describe-instances --filters "Name=tag:Name,Values=webserver" \
  --query "Reservations[].Instances[].PublicIpAddress" --output text
```
- Verified Bedrock features working (Itinerary Planner + Review Bot)

📸 `deployed-app-browser.png`
