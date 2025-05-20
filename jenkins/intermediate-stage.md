# 🚀 Intermediate Stage: Jenkins Pipelines & Automation Workflows

---

## ✅ 1. Jenkins Pipeline Basics

**🎯 Goal:**

Move from basic Freestyle jobs to code-driven, flexible automation using Pipelines.

**📌 What is a Pipeline?**

- A **Pipeline** defines the entire build process using code.
- Stored in a Jenkinsfile, version-controlled with your project.
- Two syntax styles:
  - **Declarative Pipeline** (easier, recommended)
  - **Scripted Pipeline** (more flexible, advanced use)

**🧾 Declarative Pipeline Example:**

```bash
pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/yourname/project.git'
      }
    }
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    stage('Test') {
      steps {
        sh 'npm test'
      }
    }
  }
}
```

**📍 Steps:**

- Create a **Jenkinsfile** in your repo
- In Jenkins, create a **Pipeline project**
- Configure Git repo – Jenkins auto-detects and runs the **Jenkinsfile**

---

## ✅ 2. Parameterized Builds

**🎯 Goal:**

Allow users to input values when triggering a job (e.g., environment, version).

**🔧 How:**

- Enable "This project is parameterized" in job config
- Add parameters like:
  - String Parameter – for version numbers
  - Choice Parameter – select between dev/staging/prod
  - Boolean Parameter – toggle options (e.g., run tests?)

**💡 Pipeline with Parameters:**

```bash
pipeline {
  agent any
  parameters {
    string(name: 'VERSION', defaultValue: '1.0.0', description: 'App version')
    choice(name: 'ENV', choices: ['dev', 'staging', 'prod'], description: 'Target environment')
  }
  stages {
    stage('Info') {
      steps {
        echo "Building version ${params.VERSION} for ${params.ENV}"
      }
    }
  }
}
```

---

## ✅ 3. Credentials Management

**🎯 Goal:**

Securely store and access API keys, passwords, and SSH credentials.

**🔧 Setup:**

- Go to **Manage Jenkins** → **Credentials**
- Add credentials:
  - Username & Password
  - Secret text
  - SSH private key

**💡 Using in Pipeline:**

```bash
pipeline {
  agent any
  stages {
    stage('Auth') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'my-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
          sh 'echo $USER && echo $PASS'
        }
      }
    }
  }
}
```

---

## ✅ 4. Parallel & Distributed Builds

**🎯 Goal:**

Improve performance by running jobs in parallel or on multiple Jenkins agents.

**📌 Key Concepts:**

- **Agent/Node**: Jenkins worker machine that runs jobs.
- **Labels**: Tags to assign jobs to specific types of agents (e.g., linux, windows).

**💡 Run on Specific Node:**

```bash
pipeline {
  agent { label 'linux' }
  stages {
    stage('Build') {
      steps {
        sh 'make'
      }
    }
  }
}
```

**💡 Parallel Execution:**

```bash
stage('Test') {
  parallel {
    stage('Unit Tests') {
      steps {
        sh 'npm run test:unit'
      }
    }
    stage('Integration Tests') {
      steps {
        sh 'npm run test:integration'
      }
    }
  }
}
```

---

## ✅ 5. Recommended Plugins (Intermediate Level)

| Plugin                     | Purpose                                  |
| -------------------------- | ---------------------------------------- |
| **Blue Ocean**             | Modern visual UI for Pipelines           |
| **Pipeline Utility Steps** | Useful steps for JSON/YAML/file handling |
| **Slack Notification**     | Send build alerts to Slack               |
| **AnsiColor**              | Color console logs                       |
| **GitHub Branch Source**   | Automatically build PRs and branches     |

---

## ✅ 6. Practice Projects

**💡 Project: Full CI Pipeline for Node.js**

Steps:
1. Checkout Git repository
2. Install dependencies
3. Run unit tests
4. Build and archive artifacts
5. Conditional deploy to staging

**🧾 Sample Jenkinsfile:**

```bash
pipeline {
  agent any
  environment {
    NODE_ENV = 'test'
  }
  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/yourname/node-ci-demo.git'
      }
    }
    stage('Install') {
      steps {
        sh 'npm ci'
      }
    }
    stage('Test') {
      steps {
        sh 'npm test'
      }
    }
    stage('Build') {
      steps {
        sh 'npm run build'
      }
    }
    stage('Archive') {
      steps {
        archiveArtifacts artifacts: 'dist/**/*', fingerprint: true
      }
    }
  }
}
```

---
