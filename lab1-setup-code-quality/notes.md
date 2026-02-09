# Lab 1: Code Quality & Testing – TravelGuideAI

## ✅ Objective
- Set up and run a Flask-based travel app in the AWS-provided VS Code IDE.
- Run PyLint, unit tests, and coverage report.
- Fix code quality issues and raise test coverage from 96% → 100%.

---

## Task 1: Inspect DynamoDB Tables

- Viewed **Cities** table (metadata about cities used by the app).
- Viewed **CityReviews** table (user reviews linked to each city).
- Verified that DynamoDB provides the application’s dynamic content.

📸 `dynamodb-tables.png`, `cities-table-items.png`, `cityreviews-table-items.png`

---

## Task 2: Clone and Run the Application

- Logged into the AWS lab VS Code workspace.
- Cloned the provided Git repository using the private Git URL.
- Verified required Python packages (Flask, boto3, pylint, coverage, etc.).
- Ran the Flask web application locally:
  - URL: **http://127.0.0.1:5000/**
- Confirmed UI loads city selection, “Top things to do,” and city reviews.

📸 `git-clone-output.png`, `pip-show-output.png`, `flask-run-browser.png`, `ide-screenshot.png`

---

## Task 3: Improve Code Quality and Coverage

### ✅ Before Fixes:
- **PyLint score:** 9.75/10  
  - Missing docstring in `app.py`  
  - Unused `math` import  
- **Code coverage:** 96%  
  - Uncovered lines in `load_city()` and in `city_route()` 404 branch  

### ✅ Fixes Applied:
- Removed unused import (`math`)
- Added docstring to `load_city()`
- Updated `test_city_detail_404()` to simulate missing city → return 404

### ✅ After Fixes:
- **PyLint score:** 10/10  
- **Coverage:** 100%

📸 `pylint-before-fix.png`, `pylint-after-fix.png`, `coverage-report-100.png`

---

## Task 4: Commit & Push Changes

- Staged, committed, and pushed updates using lab-provided Git credentials.
- Verified successful push to the hosted repository.

📸 `git-push-success.png`

## ✅ Summary
Successfully:
- Ran Flask application locally  
- Analyzed and fixed code quality issues  
- Achieved 100% unit test coverage  
- Committed updated code to source control  