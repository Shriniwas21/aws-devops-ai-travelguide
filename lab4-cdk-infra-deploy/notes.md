# Lab 4: Infrastructure Deployment with AWS CDK – TravelGuideAI

## ✅ Objective
- Use Python-based AWS CDK code to define infrastructure for the TravelGuideAI app.
- Synthesize and deploy the infrastructure via CloudFormation.
- Deploy the application through the existing CI/CD pipeline to the new EC2 instance.

---

## Task 1: Add CDK Application Files

- Extracted CDK update archive:
  ```bash
  unzip -o ~/update.zip
  ```

### 📁 Added Files:
- `cdk/.gitignore` – Ignore temp files for CDK
- `cdk/app.py` – Defines VPC, IAM role, EC2, permissions, outputs
- `cdk/cdk.json` – CDK app settings
- `requirements-dev.txt` – CDK Python dependencies

### 📸 Screenshots:
- `cdk-file-structure.png`, `source-control-cdk-files.png`

---

## Task 2: Deploy Infrastructure with CDK

- Installed dependencies:
  ```bash
  pip3 install -r requirements-dev.txt
  ```

- Synthesized CloudFormation template:
  ```bash
  cd cdk
  cdk synth
  ```

- Deployed stack via CDK:
  ```bash
  cdk deploy
  ```

  - Confirmed prompt with `y`
  - Observed `Stack.InstanceHttpUrl` output in terminal

- Visited EC2 URL in browser (nginx default page shown)

### 📸 Screenshots:
- `cdk-deploy-output.png`, `nginx-before-deploy.png`, `cloudformation-stack-output.png`

---

## Task 3: Deploy App to CDK-Created EC2 via CI/CD

- Initially, the `travelapp-pipeline` failed in the **Deploy** stage:
  - ❌ Error: _"No instances found for your deployment group."_
  - Root cause: EC2 instance didn't exist at first deployment attempt.
- After deploying the CDK stack (Task 2), a new EC2 instance was provisioned and tagged appropriately.
- Returned to **CodePipeline**, released a new change:
  ```text
  Release change → Pipeline re-executed
  ```

- ✅ **Build** and **Deploy** stages succeeded on retry.
- Refreshed EC2 public URL — application successfully deployed.

### 📸 Screenshots:
- `codepipeline-failure-before-cdk.png`, `codepipeline-succeeded.png`, `flask-app-after-cdk-deploy.png`
