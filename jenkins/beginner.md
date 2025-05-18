# 🟢 Jenkins Beginner Roadmap

## 🎯 Goal

Understand Jenkins fundamentals, set it up, and create your first CI job.

---

## 1. ✅ CI/CD Fundamentals

### 📚 Learn:

- What is CI (Continuous Integration)?
- What is CD (Continuous Delivery/Deployment)?
- Benefits of automation in software delivery
- Where Jenkins fits into the CI/CD pipeline

### 💡 Real-World Value:

Jenkins helps automate builds, tests, and deployments to reduce human error and speed up development.

---

## 2. 🔧 Install Jenkins

### 🖥️ Options:

- **Local installation** (Windows/macOS/Linux)
- **Docker-based installation** *(recommended)*:
```bash
docker run -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts
```

### 📌 Setup Steps:

1. Access Jenkins at: http://localhost:8080
2. Get initial admin password:
```bash
docker exec -it <container_id> cat /var/jenkins_home/secrets/initialAdminPassword
```
3. Install recommended plugins
4. Create your admin user

## 3. 🧭 Explore Jenkins UI

### 🖱️ Sections to Understand:

- Dashboard
- New Item (create jobs)
- Build History
- Manage Jenkins
- Plugin Manager

## 4. ⚙️ Create Your First Freestyle Job

### 🛠️ Steps:

1. Click New Item → Name: FirstJob
2. Choose Freestyle Project
3. Add a Build Step:
```bash
echo "Hello, Jenkins!"
```
4. Save and click Build Now
5. Check Console Output

## 5. 🔗 Source Code Integration (GitHub)

### 🛠️ Steps:

1. Create a public GitHub repo with a script:
```bash
echo "Jenkins Test Script" > test.sh
chmod +x test.sh
```
2. Push to GitHub
3. In Jenkins:
- Enable Git under Source Code Management
- Add your repo URL
- Add credentials if needed
- Add a build step to run:
```bash
./test.sh
```

## 6. 📅 Build Triggers

### 🔄 Trigger Options:

- Manual (default)
- Poll SCM:
```bash
H/5 * * * *
```
- GitHub Webhook:
  - GitHub → Settings → Webhooks
  - Payload URL: http://<jenkins-url>/github-webhook/

## 7. 🧩 Install Useful Plugins

### 🔌 Essential Plugins:

- Git
- Pipeline
- Blue Ocean
- Email Extension
- Credentials Binding

### 🛠️ Install:

1. Manage Jenkins → Manage Plugins
2. Search, select, and install

## 8. 🧼 Basic Maintenance & Security

- Backup Jenkins (JENKINS_HOME folder)
- Keep plugins and Jenkins core updated
- Use secure credentials (avoid hardcoding secrets)
- Set up Role-Based Access Control (RBAC)

## 🧪 Mini Project: "Hello Jenkins CI"

1. Create GitHub repo with hello.sh:
```bash
#!/bin/bash
echo "Hello from Jenkins CI"
```
2. Create Freestyle job in Jenkins:
- Pull from repo
- Run the script
3. Configure webhook in GitHub
4. Make a commit to trigger the build automatically

## 📋 Beginner Checklist

| Task                 | Status |
| -------------------- | ------ |
| Understand CI/CD     | ☐      |
| Install Jenkins      | ☐      |
| Explore Jenkins UI   | ☐      |
| Create Freestyle Job | ☐      |
| GitHub Integration   | ☐      |
| Build Triggers       | ☐      |
| Install Plugins      | ☐      |
| Run First CI Job     | ☐      |
| Webhook Integration  | ☐      |

## 📘 Suggested Resources

- Jenkins Documentation (https://www.jenkins.io/doc/)
- Jenkins GitHub (https://github.com/jenkinsci)

✅ Once you're confident with these steps, you're ready to move on to Pipelines in the Intermediate stage.
