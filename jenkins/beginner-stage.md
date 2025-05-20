# 🔰 Beginner Stage: Jenkins Introduction & Basic Usage

---

## ✅ 1. What is Jenkins? (And Why Use It)

**🎯 Goal:**

Understand what Jenkins is and why it's used in modern software development.

**📌 Key Concepts:**

- Jenkins is an open-source automation server used to automate parts of the software development process.
- It’s commonly used for Continuous Integration (CI) and Continuous Delivery (CD).
- Helps teams automate code pulling, building, testing, and deploying.

**💡 Example:**

Whenever you push code to GitHub, Jenkins can automatically fetch the code, run tests, and send you the results.

---

## ✅ 2. Installing Jenkins

**🎯 Goal:**

Set up Jenkins and access the web dashboard.

**🔧 Recommended Installation Methods:**

| Method | Best For | Command / Steps |
| --- | --- | --- |
| **Docker** (✅ Recommended) | Fast setup, clean test environments      | `docker run -p 8080:8080 jenkins/jenkins:lts` |
| **Native Install**          | Long-term or production use              | Download `.war`, `.msi`, or `.pkg` from [https://www.jenkins.io/download](https://www.jenkins.io/download) and install accordingly. |
| **WAR File**                | Lightweight, portable, no install needed | `java -jar jenkins.war` |

**🚀 First-Time Setup:**

- Access http://localhost:8080
- Enter admin password (from file or Docker logs)
- Install suggested plugins
- Create an admin user

---

## ✅ 3. Jenkins Web Interface Overview

**🎯 Goal:**

Get familiar with Jenkins dashboard and key navigation areas.

**🖥️ Key Sections:**

- Dashboard: Your list of jobs
- Manage Jenkins: Global config and plugin manager
- New Item: Create a new job
- Build History: View logs of past runs

---

## ✅ 4. Create Your First Job (Freestyle Project)

**🎯 Goal:**

Create a basic Jenkins job, connect to Git, and automate a build step.

**🛠 Steps:**

1. Click “New Item” → Name your job → Choose Freestyle project
2. Configure:
- Source Code Management: Use Git, e.g. https://github.com/yourname/yourproject.git
- Build Triggers: How the build is triggered (manually, on schedule, or on Git changes)
- Build Steps: Shell script or batch file Example: npm install && npm test
- Post-build Actions: Email, archive artifacts, etc.

**🧪 Practice Suggestion:**

- Create a repo with a simple script like:
```bash
echo "Hello, Jenkins!"
```
- Create a job that pulls this repo and runs it.

---

## ✅ 5. Plugin Management

**🎯 Goal:**

Learn how to extend Jenkins functionality.

**📦 How to Manage Plugins:**

- Go to Manage Jenkins → Plugin Manager
- You can install, update, or remove plugins.

**🔌 Useful Plugins:**

| Plugin Name      | Purpose                      |
| ---------------- | ---------------------------- |
| Git Plugin       | Enable Git repo support      |
| Pipeline Plugin  | Enable Pipeline jobs         |
| Email Extension  | Advanced email notifications |
| AnsiColor Plugin | Color output in console log  |

---

## ✅ 6. Build Notifications & Artifacts

**📧 Email Notification:**

- Configure SMTP in: Manage Jenkins → Configure System
- Add email post-build actions in the job.


**📂 Archive Build Artifacts:**

- Example: Save generated .zip, .jar, or .log files after build.

---

## ✅ 7. Practice Projects

**💡 Project 1: Hello Jenkins**

- Create a Git repo with:
```bash
print("Hello, Jenkins!")
```
- Jenkins job steps:
  - Git pull
  - Shell step: python3 hello.py
  - Success = log prints "Hello, Jenkins!"

---

## ✅ Summary: What You Should Know After This Stage

| Topic                            | Status ✅ |
| -------------------------------- | -------- |
| Understand Jenkins & CI/CD       | ✅        |
| Install Jenkins & access UI      | ✅        |
| Create & run Freestyle Jobs      | ✅        |
| Pull code from Git               | ✅        |
| Execute build/test scripts       | ✅        |
| Install & use plugins            | ✅        |
| Send email and save build output | ✅        |

---
