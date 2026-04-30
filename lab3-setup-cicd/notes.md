# Lab 3: CI/CD Pipeline Setup – TravelGuideAI

## ✅ Objective
- Add CodeBuild and CodeDeploy configuration files to the project.
- Create AWS CodeBuild and CodeDeploy resources.
- Set up a CI/CD pipeline using AWS CodePipeline.
- Automate build, test and deployment to EC2.
- Verify deployment via pipeline execution.

---

## Task 1: Initialize Repo & CI/CD Configs

- Cloned repository:
  ```bash
  bash ~/clone_repo.sh
  ```

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
- `repo-clone-output.png`, `source-control-changes.png`, `terminal-unzip-output.png`

---

## Task 2: Create CodePipeline (CI Stage)

- Created pipeline: `travelapp-pipeline`
- Configured with:
  - Source: Custom Git repo
  - Build: AWS CodeBuild (`ContinuousIntegration` project)
    - Role: `CodeBuildRole`
    - Buildspec: `buildspecs/integration.yaml`

### 🔧 Observations:
- ✅ PyLint passed (10/10)
- ✅ All 6 unit tests passed
- ✅ Code coverage reports visible

### 📸 Screenshots:
- `codebuild-logs.png`, `pipeline-stages-success.png`, `coverage-report.png`

---

## Task 3: Create CodeDeploy Project

- Created Application: `TravelApp`
- Created Deployment Group: `InstancesGroup`
  - EC2 Tag: `Name = travel-app`
  - Role: `CodeDeployRole`
  - Load balancer: `Disabled`

### 📸 Screenshots:
- `codedeploy-app-config.png`, `deployment-group-config.png`

---

## Task 4: Update CodePipeline with Deploy Stage

- Added new stage: `Deploy`
- Configured CodeDeploy deployment group in CodePipeline
- Accessed the EC2 instance using the provided `WebServerURL`
- Observed default NGINX welcome page (application not yet deployed)
- Triggered deployment via `Release change`
- The application was deployed to EC2 via CodeDeploy.
- Accessed the deployed application using EC2 public URL and it was successfully loaded.

### 📸 Screenshots:
- `pipeline-with-deploy.png`, `nginx-default-page.png`,  `codedeploy-success.png`, `app-browser-view.png`

---

## Task 5: Trigger Auto Deployment via Release change

- Applied Update:
  ```bash
  unzip -o ~/update2.zip
  ```

- Triggered pipeline after commit via `Release change`
  ```bash
  git add .
  git commit -m "Updated the application background image"
  git push
  ```

- Verified pipeline stages triggered via `Release change`
- ✅ Build + Deploy stages succeeded
- ✅ Changes reflected in browser

### 📸 Screenshots:
- `updated-app-commit.png`, `codepipeline-success.png`, `updated-app-ui.png`

## ✅ Summary
Successfully:
- Implemented CI/CD pipeline using AWS Codepipeline
- Automated build (CodeBuild) and deployment (CodeDeploy)
- Verified application deployment via browser