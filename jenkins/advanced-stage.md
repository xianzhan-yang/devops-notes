# 🧠 Advanced Stage: Jenkins for Scalable, Secure, and Enterprise Automation

## ✅ 1. Shared Libraries (Reusable Pipeline Code)

**🎯 Goal:**

Avoid repeating code across Jenkinsfiles by creating custom, version-controlled pipeline libraries.

**📌 Key Concepts:**

- Shared libraries allow you to define:
  - Common functions (e.g., deployApp())
  - Custom steps and utilities
- Located in a separate Git repo, loaded into Jenkins globally

**📁 Structure:**

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

**📄 Example (vars/sayHello.groovy):**

```groovy
def call(String name = 'World') {
    echo "Hello, ${name}!"
}
```

**📄 In your Jenkinsfile:**

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

## ✅ 2. Jenkins + Docker Integration

**🎯 Goal:**

Run builds inside Docker containers or use Jenkins to build/push Docker images.

**🔧 Use Cases:**

- Isolate environments
- Build and test inside containers
- Publish to DockerHub or private registry

**🧾 Example: Build Docker Image in Pipeline**

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

## ✅ 3. Jenkins + Kubernetes Integration (Jenkins X / Cloud-native)

**🎯 Goal:**

Scale Jenkins agents dynamically using Kubernetes and deploy apps to K8s clusters.

**✅ Approaches:**

- Use the Kubernetes plugin to spawn Jenkins agents (Pods) on-demand.
- Deploy Jenkins inside Kubernetes as a service (via Helm).
- Use Kubernetes secrets/configmaps inside your pipeline.

**🧾 Sample Agent Declaration:**

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
