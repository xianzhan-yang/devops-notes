# Intermediate Stage: GitLab CI/CD & Pipelines

**Goal**

Master GitLab CI/CD fundamentals:

- Define pipelines using .gitlab-ci.yml
- Automate build/test/deploy tasks
- Understand runners, stages, jobs, and artifacts

---

## 1. How GitLab CI/CD Works

GitLab CI/CD runs jobs using a file named .gitlab-ci.yml in your repository’s root.

When you push code:

- GitLab reads .gitlab-ci.yml
- Sends jobs to a **GitLab Runner**
- Executes jobs in defined stages (e.g., build → test → deploy)

---

## 2. Basic .gitlab-ci.yml Structure

```yaml
stages:
  - build
  - test
  - deploy

build_job:
  stage: build
  script:
    - echo "Building app..."
    - npm install

test_job:
  stage: test
  script:
    - echo "Running tests..."
    - npm test

deploy_job:
  stage: deploy
  script:
    - echo "Deploying app..."
```

---

## 3. GitLab Runners

What is a Runner?

A Runner is a GitLab agent that runs your CI jobs.

- **🖥️ Shared Runner**: Provided by GitLab.com
- **🧰 Specific Runner**: Self-hosted, configured to run for a project/group
- **🐳 Docker-based Runner**: Most popular and isolated

Register your own Runner (optional):

```bash
gitlab-runner register
```

---

## 4. Common CI/CD Keywords

| Key                       | Description                       |
| ------------------------- | --------------------------------- |
| `stages`                  | Defines pipeline flow             |
| `script`                  | The shell commands to run         |
| `only`, `except`, `rules` | When to run the job               |
| `artifacts`               | Files saved after a job           |
| `cache`                   | Speeds up builds by reusing files |
| `environment`             | Used for deploy previews          |
| `tags`                    | Match job to specific Runner      |

---

## 5. Real Example: Node.js App CI/CD

```yaml
image: node:18

stages:
  - install
  - test
  - deploy

install_dependencies:
  stage: install
  script:
    - npm install
  cache:
    paths:
      - node_modules/

run_tests:
  stage: test
  script:
    - npm test
  artifacts:
    when: always
    paths:
      - test-results.xml

deploy_to_staging:
  stage: deploy
  script:
    - ./deploy.sh staging
  only:
    - main
```

---

## 6. CI/CD Variables and Secrets

- Go to: **Project** → **Settings** → **CI/CD** → **Variables**
- Store tokens, API keys, passwords (never hardcode secrets!)
- Use them in jobs like this:

```yaml
script:
  - curl -H "Authorization: Bearer $DEPLOY_TOKEN" ...
```

---

## 7. Pipeline Triggers

| Trigger       | Use Case             |
| ------------- | -------------------- |
| Push          | Default trigger      |
| Merge Request | Auto-run tests on PR |
| Schedule      | Nightly builds       |
| Manual        | For deploy approvals |

Example: Manual Trigger

```yaml
manual_deploy:
  stage: deploy
  script: ./deploy-prod.sh
  when: manual
  only:
    - main
```

---

## 8. Artifacts vs Cache

| Feature     | Use Case                                           |
| ----------- | -------------------------------------------------- |
| `artifacts` | Save job outputs (e.g., test results) between jobs |
| `cache`     | Speed up builds (e.g., cache dependencies)         |

---

## 9. Reusable Jobs with extends and include

- Modularize pipelines across projects using include
- DRY your jobs using extends

```yaml
.default-job-template:
  script:
    - echo "Do something"

job1:
  extends: .default-job-template
```

---

## 10. Practice Project

CI for a Frontend App

- Add a .gitlab-ci.yml that:
  - Installs dependencies
  - Runs unit tests
  - Lints code
  - Deploys to GitLab Pages or Netlify on main

---
