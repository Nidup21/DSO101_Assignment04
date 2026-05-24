# DSO101 Assignment 4 — CI/CD Pipeline with Testing & Deployment

## Overview

This project implements a complete CI/CD pipeline for a simple Flask-based Hello World API. The pipeline automatically installs dependencies, runs unit tests, and deploys the application to Render.com on every push to the `main` branch. The project was built from scratch using Python, Flask, and pytest.

---

## Tech Stack

| Tool | Purpose |
|---|---|
| GitHub | Source code hosting |
| GitHub Actions | CI/CD automation |
| Python & Flask | Backend runtime and web framework |
| pytest | Unit testing framework |
| Render.com | Cloud deployment |

---

## Project Structure

```
dso101-assignment4/
├── app.py
├── test_app.py
├── requirements.txt
└── .github/
    └── workflows/
        └── ci.yml
```

---

## Application

The app is a minimal REST API built with Flask, exposing two endpoints:

| Endpoint | Method | Response |
|---|---|---|
| `/` | GET | `{"message": "Hello, World!"}` |
| `/health` | GET | `{"status": "ok"}` |

---

## Steps Taken

### 1. Project Setup
- Created a new public GitHub repository named `dso101-assignment4`.
- Cloned the repository locally on macOS and set up a Python virtual environment using `python3 -m venv venv` to isolate dependencies.
- Added `venv/`, `__pycache__/`, and `.pytest_cache/` to `.gitignore` to keep the repository clean.

### 2. Application Development
- Built a minimal Flask API in `app.py` with two routes: a home route returning a Hello World JSON response and a health check route.
- Created `requirements.txt` listing `flask` and `pytest` as dependencies.

### 3. Unit Testing
- Wrote two unit tests in `test_app.py` using pytest and Flask's built-in test client.
- `test_home` verifies that the home route returns HTTP 200 and the correct JSON body.
- `test_health` verifies that the health route returns HTTP 200 and a status of `ok`.
- Ran tests locally using `python3 -m pytest` to confirm both passed before pushing.

### 4. CI/CD Pipeline
- Created `.github/workflows/ci.yml` at the repository root.
- The workflow triggers on every push to `main` and runs four sequential steps: checkout, Python setup, dependency installation, test execution, and Render deployment trigger.
- The deploy step only executes if all tests pass, ensuring broken code is never deployed.

### 5. Render Deployment
- Created a new Web Service on Render.com connected to the GitHub repository.
- Configured the build command as `pip install -r requirements.txt` and the start command as `python app.py`.
- Retrieved the Deploy Hook URL from Render's service settings and stored it securely as a GitHub Actions secret named `RENDER_DEPLOY_HOOK`.

### 6. Final Push & Verification
- Pushed all files to the `main` branch, triggering the workflow automatically.
- Verified each step completed successfully in the GitHub Actions tab.
- Confirmed the live app was accessible at the Render deployment URL.

---

## Challenges Faced

The project was completed without any major issues. Setting up the virtual environment on macOS and using `python3` and `pip3` commands (rather than `python` and `pip`) ensured compatibility with the system's Python installation. The GitHub Actions runner uses Ubuntu, so the CI environment required no special configuration beyond what was already in the workflow file.

---

## Learning Outcomes

- Learned how to build and structure a minimal Python Flask API suitable for CI/CD integration.
- Gained practical experience writing unit tests with pytest using Flask's test client to verify API route behaviour.
- Understood how to design a CI/CD pipeline where deployment is conditional on passing tests — a core principle of reliable DevOps workflows.
- Learned how to securely pass deployment credentials into GitHub Actions using repository secrets, avoiding hardcoded values.
- Understood how Render Deploy Hooks work and how to integrate them as the final step of an automated pipeline.

---

