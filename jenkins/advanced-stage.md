# Advanced Stage: Jenkins for Scalable, Secure, and Enterprise Automation

---

## 1. Shared Libraries (Reusable Pipeline Code)

Goal:
Avoid repeating code across Jenkinsfiles by creating **custom**, **version-controlled pipeline libraries**.

Key Concepts:
- Shared libraries allow you to define:
  - Common functions (e.g., deployApp())
  - Custom steps and utilities
- Located in a separate Git repo, loaded into Jenkins globally

Structure:
```text
(root)
├── vars/
│   └── sayHello.groovy   # Simple custom step
├── src/
│   └── org/mycompany/
│       └── tools/Helper.groovy
└── resources/
    └── templates/deploy.yaml
```

Example (vars/sayHello.groovy):
```groovy
def call(String name = 'World') {
    echo "Hello, ${name}!"
}
```

In your Jenkinsfile:
```groovy
@Library('my-shared-lib') _
pipeline {
  agent any
  stages {
    stage('Greeting') {
      steps {
        sayHello('Jenkins Pro')
      }
    }
  }
}
```

---

## 2. Jenkins + Docker Integration

Goal:
Run builds **inside Docker containers** or use Jenkins to **build/push Docker images**.

Use Cases:
- Isolate environments
- Build and test inside containers
- Publish to DockerHub or private registry

Example: Build Docker Image in Pipeline
```groovy
pipeline {
  agent any
  stages {
    stage('Build Image') {
      steps {
        script {
          docker.build("myapp:${env.BUILD_ID}")
        }
      }
    }
    stage('Push') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
          sh "echo $PASS | docker login -u $USER --password-stdin"
          sh "docker push myapp:${env.BUILD_ID}"
        }
      }
    }
  }
}
```

---

## 3. Jenkins + Kubernetes Integration (Jenkins X / Cloud-native)

Goal:
Scale Jenkins agents dynamically using Kubernetes and deploy apps to K8s clusters.

Approaches:
- Use the **Kubernetes plugin** to spawn Jenkins agents (Pods) on-demand.
- Deploy Jenkins inside Kubernetes as a service (via Helm).
- Use Kubernetes secrets/configmaps inside your pipeline.

Sample Agent Declaration:
```groovy
pipeline {
  agent {
    kubernetes {
      yaml """
      apiVersion: v1
      kind: Pod
      spec:
        containers:
        - name: jnlp
          image: jenkins/inbound-agent
        - name: node
          image: node:18
          command:
          - cat
          tty: true
      """
    }
  }
  stages {
    stage('Test') {
      steps {
        container('node') {
          sh 'node -v'
        }
      }
    }
  }
}
```

---

## 4. Dynamic Pipelines & Templating

Goal:
Generate pipelines dynamically or drive behavior with configuration files (YAML/JSON).

Use Cases:
- Multi-project pipeline template
- Environment-driven stages

Technique:
Use **load**, **evaluate**, or JSON/YAML parsers to drive logic.
Example: Load pipeline steps from JSON
```groovy
def config = readJSON file: 'pipeline.json'
for (stage in config.stages) {
    stage(stage.name) {
        steps {
            sh stage.command
        }
    }
}
```

---

## 5. Jenkins Configuration as Code (JCasC)

Goal:
Version-control Jenkins setup (users, jobs, plugins) using YAML.

Plugin:
- **Configuration as Code (JCasC)** plugin
Example: jenkins.yaml
```yaml
jenkins:
  systemMessage: "Configured by JCasC"
  securityRealm:
    local:
      allowsSignup: false
      users:
        - id: "admin"
          password: "admin123"
  authorizationStrategy:
    loggedInUsersCanDoAnything:
      allowAnonymousRead: false
```
- Auto-load with:
java -Djenkins.install.runSetupWizard=false -Dcascade.config=jenkins.yaml -jar jenkins.war

---

## 6. Security Hardening (Advanced Best Practices)

Key Topics:
- Use **folders and role-based access control (RBAC)** via plugins
- Use **Credentials Binding** (never hardcode secrets)
- Enable **audit logging**
- Limit agent shell access
- Use **HTTPS**, reverse proxy, and firewalls
- Run Jenkins with **limited privileges**
- Regularly update plugins and Jenkins core

---

## 7. Enterprise CI/CD Patterns

Strategies:
- **Multi-branch pipelines**: Automatically build every branch or PR
- **Matrix builds**: Test across OS, Node.js versions, etc.
- **Approval gates**: Require manual approval for production deploy
- **Audit-ready logging**: Centralized log collection (e.g., ELK stack)
- **Integration with GitHub/GitLab/Bitbucket**, Slack, Jira

---

## 8. Practice Projects

Project 1: Docker-based CI/CD
- Build & test app inside Docker container
- Push image to DockerHub
- Deploy image to staging via SSH

Project 2: Kubernetes Native Pipeline
- Jenkins deployed in K8s
- Pipeline builds Helm chart & deploys to dev cluster

Project 3: Shared Library CI
- Extract repeated stages (checkoutCode, buildApp) to a shared repo
- Use in 3 different pipelines

---
