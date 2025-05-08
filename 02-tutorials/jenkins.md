# Install

---

## Install Jenkins on Linux

### Add Alibaba Repository (Only in China)

```bash
sudo sed -e 's|^mirrorlist=|#mirrorlist=|g' -e 's|^#baseurl=http://dl.rockylinux.org/$contentdir|baseurl=https://mirrors.aliyun.com/rockylinux|g' -i.bak /etc/yum.repos.d/rocky*.repo
```
```bash
sudo yum makecache
```

### Add Jenkins Repository

```bash
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
```
```bash
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
```

### Update Software

```bash
sudo yum upgrade
```

### Install Java

```bash
sudo yum install fontconfig java-21-openjdk
```

### Install Jenkins

```bash
sudo yum install jenkins
```

### Start Jenkins

```bash
sudo systemctl enable jenkins
```
```bash
sudo systemctl start jenkins
```

### Add Port

```bash
sudo firewall-cmd --add-port=8080/tcp --permanent
```
```bash
sudo firewall-cmd --reload
```
## Install Jenkins on Docker

```bash
continue...
```

---

# Initial

---

## Unlock Jenkins

![image](assets/images/unlock-jenkins.png)

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

## Customize Jenkins

![image](assets/images/customize-jenkins.png)

## Create First Admin User

![image](assets/images/create-first-admin-user.png)

## Instance Configuration

![image](assets/images/instance-configuration.png)

---

# Manage Jenkins

## Security

### Credentials

![image](assets/images/add-credentials.png)
![image](assets/images/new-credentials.png)

## System Configuration

### System 

#### GitLab

![image](assets/images/gitlab.png)
![image](assets/images/test-connection.png)

---

# New Item

## Pipeline

![image](assets/images/new-item.png)
![image](assets/images/gitlab-connection.png)

GitLab webhook URL is very important, we will use in GitLab configuration

![image](assets/images/triggers.png)
![image](assets/images/pipeline.png)

---
