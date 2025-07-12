# Lab 3: CI/CD Pipeline Setup – TravelGuideAI

## ✅ Objective
- Add CodeBuild and CodeDeploy configuration files to the project.
- Create AWS CodeBuild and CodeDeploy resources.
- Set up a CI/CD pipeline using AWS CodePipeline to deploy the TravelGuideAI app to EC2.
- Verify deployment by triggering changes through version control.

---

## Task 1: Add CodeBuild and CodeDeploy Configs

- Extracted update archive:
  ```bash
  unzip -o ~/update.zip
  ```

### 📁 Added Files:
- `appspec.yml` – Lifecycle hooks for CodeDeploy
- `buildspecs/integration.yaml` – CodeBuild configuration
- `scripts/install_application` – Install script for EC2 instance
- `scripts/start_server` – Starts the application
- `scripts/stop_server` – Stops the application

### 📸 Screenshots:
- `source-control-changes.png`, `terminal-unzip-output.png`

---

## Task 2: Create CodePipeline (CI Only)

- Created pipeline: `travelapp-pipeline`
- Configured with:
  - Source: Custom Git repo
  - Build: AWS CodeBuild (`ContinuousIntegration` project)
    - Role: `CodeBuildRole`
    - Buildspec: `buildspecs/integration.yaml`

### 🔧 Observations:
- ✅ PyLint ran with success
- ✅ All 6 unit tests passed
- ✅ Code coverage reports visible

### 📸 Screenshots:
- `codebuild-logs.png`, `pipeline-stages-success.png`

---

## Task 3: Create CodeDeploy Project

- Created Application: `TravelApp`
- Created Deployment Group: `InstancesGroup`
  - EC2 Tag: `Name = travel-app`
  - Role: `CodeDeployRole`

### 📸 Screenshots:
- `codedeploy-app-config.png`

---

## Task 4: Update CodePipeline with Deploy Stage

- Added new stage: `Deploy`
- Configured CodeDeploy deployment group in CodePipeline
- Triggered deployment
- The application was deployed to EC2 via CodeDeploy. While direct browser access was restricted due to security group limits, deployment logs confirmed success.

### 📸 Screenshots:
- `pipeline-with-deploy.png`, `codedeploy-complete.png`

---

## Task 5: Trigger Auto Deployment via Git Push

- Updated background image:
  ```bash
  unzip -o ~/update2.zip
  git add .
  git commit -m "Updated the application background image"
  git push
  ```

- Verified pipeline stages auto-triggered
- ✅ Build + Deploy stages succeeded
- ⚠️ Due to lab security group restrictions, browser verification was not possible. Verified deployment success through logs.

### 📸 Screenshots:
- `codepipeline-auto-deploy.png`, `codedeploy-logs-success.png`
