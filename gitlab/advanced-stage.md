# 🔴 Advanced Stage: GitLab CI/CD at Scale

**🎯 Goal:**

Gain deep proficiency in GitLab CI/CD by mastering:
    
- Advanced pipeline features
- Microservice and monorepo CI strategies
- Kubernetes integration
- GitOps workflows
- Secure and scalable deployment practices

---

## 1. 🧱 Dynamic & Multi-Project Pipelines

**🔁 Parent–Child Pipelines**

Split complex pipelines into smaller parts:

```yaml
trigger_child:
  stage: test
  trigger:
    include: child-pipeline.yml
```

**🧩 Multi-Project Pipelines**

Coordinate multiple services:

```yaml
trigger_remote:
  trigger:
    project: my-group/other-service
    branch: main
```

---

## 2. 🗂️ Pipeline Templates & Includes

**🔄 Reusability with include**

Share jobs across projects:

```yaml
include:
  - project: 'devops/templates'
    file: '/ci-templates/test.yml'
```

**🧪 Use Cases:**

- Standardize build/deploy steps
- Centralize security scans
- Enforce naming and job conventions

---

## 3. ☸️ Kubernetes Integration

**🔧 Setup:**

- Register GitLab Kubernetes agent or use GitLab-managed cluster integration
- Add Kube config to CI/CD variables or use GitLab’s K8s agent

**Example Deploy Job:**

```bash
deploy_to_k8s:
  stage: deploy
  script:
    - kubectl apply -f k8s/deployment.yaml
  environment:
    name: production
```

**🔄 Auto DevOps (optional):**

- GitLab can auto-detect app type
- Provides build, test, code quality, review apps, deploy to K8s

---

## 4. 🔐 Security & Compliance

| Feature                 | Description                       |
| ----------------------- | --------------------------------- |
| **SAST**                | Static analysis (code scan)       |
| **DAST**                | Dynamic app security testing      |
| **Dependency Scanning** | CVE checks                        |
| **License Compliance**  | Detect GPL/MIT/etc.               |
| **Secret Detection**    | Warn on tokens, passwords in code |

**Example:**

```yaml
include:
  - template: Security/SAST.gitlab-ci.yml
  - template: Security/Secret-Detection.gitlab-ci.yml
```

---

## 5. 🔍 Observability and Control

**📈 Pipeline Insights**

- GitLab UI: “CI/CD → Analytics”
- View pipeline success rates, durations

**✅ Pipeline Rules & Conditions**

Smart control over pipeline logic:

```yaml
job:
  script: run.sh
  rules:
    - if: '$CI_COMMIT_BRANCH == "main"'
      when: always
    - if: '$CI_COMMIT_TAG'
      when: manual
```

---

## 6. 🤖 GitOps Workflows with GitLab

**🔁 Git as the source of truth:**

- Merge request triggers deployment
- Infra code in version control (e.g., Terraform, Helm, Kustomize)
- Use tools like:
  - Argo CD
  - Flux
  - GitLab K8s agent

---

## 7. 🧠 AI & Automation Enhancements

- **Code Suggestions in MRs**
- **Auto-resolving vulnerabilities**
- **Bot-based reviews**
- Use GitLab APIs to auto-open MRs or manage users/pipelines

---

## 8. 🧪 Practice Projects

| Project              | Description                                       |
| -------------------- | ------------------------------------------------- |
| 🔗 Multi-Project CI  | Trigger backend after frontend pipeline           |
| ☸️ K8s GitOps        | Use GitLab agent to deploy changes to K8s         |
| 🔐 Secure Pipeline   | Add SAST, Secret Detection, and License Scan      |
| 📂 Monorepo Pipeline | Use dynamic includes for selective service builds |

---

## 9. 📚 Optional: Self-Managed GitLab

Learn GitLab server architecture:

- PostgreSQL, Gitaly, Redis, Puma
- Helm chart vs Omnibus
- LDAP & SSO integration
- Backup, restore, HA setup

---
