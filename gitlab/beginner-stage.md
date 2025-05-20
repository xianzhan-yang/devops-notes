# 🟢 Beginner Stage: GitLab Basics

**🎯 Goal:**

Understand how to use GitLab as a Git repository platform, collaborate with others, and manage your code using basic Git operations and GitLab features.

---

## 1. 🔍 What is GitLab?

GitLab is an all-in-one DevOps platform that includes:

- Git-based version control (like GitHub)
- Built-in CI/CD pipelines
- Issue tracking, code review (merge requests), security scanning, and more.

✅ You can use:

- GitLab.com (cloud-hosted)
- Or self-host it on your own server (Omnibus, Helm, etc.)

---

## 2. 🧱 Core Git Concepts (Used with GitLab)

| Term                   | Meaning                                                         |
| ---------------------- | --------------------------------------------------------------- |
| **Repository (repo)**  | Your project’s code base                                        |
| **Commit**             | A saved change                                                  |
| **Branch**             | A version of the code to work on independently                  |
| **Merge Request (MR)** | GitLab’s version of a Pull Request – propose and review changes |
| **Fork**               | A copy of a repo under your own account                         |
| **Clone**              | Download the repo to your local machine                         |

---

## 3. 🚀 Getting Started Steps 

**✅ Step 1: Create a GitLab Account**

Go to https://gitlab.com and sign up.

**✅ Step 2: Create a New Repository (Project)**

1. Click “New Project”
2. Choose Blank Project
3. Fill in name, visibility (Private/Public), and click “Create”

**✅ Step 3: Set Up Git on Your Local Machine**

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

**✅ Step 4: Connect GitLab with SSH or HTTPS**

**SSH (recommended for push access)**:

- Generate key: ssh-keygen -t ed25519
- Add public key (~/.ssh/id_ed25519.pub) in GitLab → Settings → SSH Keys

**HTTPS (simpler for read access)**:

- Use GitLab username and a Personal Access Token as password (not your GitLab password!)

---

## 4. 🛠️ Common Git Operations with GitLab

```bash
# Clone a GitLab repo
git clone git@gitlab.com:username/project.git

# Create a new branch
git checkout -b feature-xyz

# Add and commit changes
git add .
git commit -m "Add new feature"

# Push branch to GitLab
git push origin feature-xyz
```

---

## 5. 🔁 Merge Requests (MRs) – Code Review Flow

GitLab Merge Requests are like GitHub Pull Requests.

**Steps**:

- Push a new branch
- In GitLab → Create Merge Request
- Add reviewers, description, and labels
- Get approvals and merge into main

---

## 6. 🐞 Issue Tracking and Collaboration

- **Issues**: Track bugs, tasks, and features (like Jira-lite)
- **Milestones**: Group issues by release or sprint
- **Labels**: Tag issues (e.g., bug, frontend, urgent)
- **Assignees**: Assign issues to teammates
- **To-do list**: Shows your mentions and assignments

---

## 7. 📁 Other Useful GitLab Features

| Feature           | Purpose                       |
| ----------------- | ----------------------------- |
| **Readme.md**     | Markdown welcome page of repo |
| **Wiki**          | Project documentation         |
| **Snippets**      | Save reusable code            |
| **Activity Feed** | See who changed what, when    |

---

## 8. 🧪 Practice Project

**Goal**: Create a personal GitLab repo and push a local project.

**Steps**:

1. Create a new GitLab repo: my-first-project
2. Initialize a local Git repo

```bash
git init
git remote add origin git@gitlab.com:yourname/my-first-project.git
touch README.md
git add .
git commit -m "Initial commit"
git push -u origin main
```
3. Create a new branch, make a change, push, and create a Merge Request

---
