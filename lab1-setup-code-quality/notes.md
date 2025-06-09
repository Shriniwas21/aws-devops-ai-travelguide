# Lab 1: Code Quality & Testing – TravelGuideAI

## ✅ Objective
- Set up and run a Flask-based travel app locally.
- Run PyLint and unit tests.
- Fix code quality issues and increase test coverage from 96% to 100%.

---

## Task 1: Inspect DynamoDB Tables

- Explored `Cities` table — contains metadata about major cities (used in app UI).
- Explored `CityReviews` table — contains ratings and text reviews for each city.
- These tables power the dynamic content of the TravelGuideAI app.

📸 `dynamodb-tables.jpg`, `dynamodb-cities-table.jpg`, `dynamodb-cityreviews-table.jpg`

---

## Task 2: Clone and Run the Application

- Cloned lab repo into the IDE using provided Git URL.
- Verified required packages (Flask, Boto3, PyLint, etc.) were pre-installed.
- Ran the Flask app locally on http://127.0.0.1:5000
- Verified UI — city selector, city reviews, and activities displayed correctly.

📸 `flask-app-ui.jpg`, `terminal-flask-run.jpg`, `app-code.jpg`

---

## Task 3: Improve Code Quality and Coverage

### ✅ Before Fixes:
- PyLint: Score was 9.75/10 with:
  - Missing docstring in `app.py`
  - Unused import `math`
- Code coverage was 96%, missing coverage in `load_city()` and `city_route()`.

### ✅ Fixes Applied:
- Removed `math` import
- Added docstring to `load_city()`
- Enhanced `test_city_detail_404()` to simulate no match and trigger 404

### ✅ After Fixes:
- PyLint score: 10/10
- Code coverage: 100%

📸 `pylint-before.jpg`, `pylint-after.jpg`, `coverage-after.jpg`

---

## Task 4: Push Code Changes

- Committed code improvements to the repo provided by the lab.
- Git push succeeded using provided credentials.

📸 `git-push-success.jpg`