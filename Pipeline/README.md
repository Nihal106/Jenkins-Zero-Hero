# 📘Jenkins Pipelines

This module introduces **Jenkins Pipelines**, the modern way of implementing **CI/CD as code** using a file called `Jenkinsfile`.

## 🔹 1️⃣ What is a Jenkins Pipeline?

A **Jenkins Pipeline** is a **series of automated steps** that define how an application is:

- Built
- Tested
- Packaged
- Deployed

These steps are written as code in a file called:


The `Jenkinsfile` is stored inside the GitHub repository along with the application code.

---

### ✅ Advantages of Pipelines over Freestyle Jobs

| Feature | Freestyle Job | Pipeline |
|------|---------------|----------|
| Configuration | UI-based | Code-based |
| Version control | ❌ No | ✅ Yes |
| Multi-stage workflows | Hard to manage | Easy |
| Rollback | Difficult | Simple (Git) |
| Large projects | Not scalable | Easy to maintain |

👉 Pipelines implement **CI/CD as Code**, which is the industry standard.

---

## 🔹 2️⃣ Types of Jenkins Pipelines

Jenkins supports **two types of pipelines**.

---

### ✅ Declarative Pipeline
- Structured and easy to read
- Beginner-friendly
- Recommended by Jenkins

#### Uses the syntax:

```groovy
pipeline {
    ...
}
```
#### Best suited for:

* Learning Jenkins

* Standard CI/CD workflows

* Most real-world projects

### ✅ Scripted Pipeline

* Written fully in Groovy

* Highly flexible

* More complex syntax

#### Uses the syntax:
```groovy
node {
    ...
}
```

#### Best suited for:

* Advanced automation

* Complex workflows

* Custom logic

### 📌 Declarative vs Scripted (Quick Comparison)

| Declarative        | Scripted           |
| ------------------ | ------------------ |
| Simple             | Complex            |
| Structured         | Fully programmable |
| Less flexible      | Very flexible      |
| Most commonly used | Advanced use cases |


### 🔹 3️⃣ Pipeline Structure (Declarative Example)

#### Below is a simple Declarative Jenkinsfile:

```groovy
pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/yourname/jenkins-maven-demo.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
    }
    post {
        success {
            echo 'Build Successful!'
        }
        failure {
            echo 'Build Failed!'
        }
    }
}
```

#### Explanation of Sections

* pipeline – Defines the pipeline

* agent – Specifies where the pipeline runs

* stages – Contains all CI/CD stages

* stage – A single step like Build or Test

* steps – Commands executed in a stage

* post – Actions after pipeline completion


### 🔹 4️⃣ Agent / Node

#### An agent (node) is the machine where the pipeline actually runs.

#### Agent options:

| Option                       | Meaning                    |
| ---------------------------- | -------------------------- |
| `agent any`                  | Runs on Jenkins controller |
| `agent { label 'aws-node' }` | Runs on a specific node    |
| Distributed agents           | Runs on remote servers     |


#### Example using a labeled agent:

```groovy
pipeline {
    agent { label 'aws-node' }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
    }
}
```

#### Why companies use agents:

* Reduce load on Jenkins controller

* Use different OS or tools

* Scale builds horizontally

* Run jobs in parallel

* Support Docker and Kubernetes builds

### 🔹 5️⃣ Multibranch Pipeline

#### A Multibranch Pipeline automatically discovers all branches in a GitHub repository.

#### Example repository branches:
```
main
dev
feature-login
feature-payment
```

Jenkins automatically creates separate jobs for each branch.

#### Key points:

* Each branch must contain a 'Jenkinsfile'

* Builds trigger automatically on push

* Ideal for Git workflows and teams

### 🔹 6️⃣ GitHub Webhook Integration

#### A GitHub Webhook allows Jenkins to automatically trigger builds when code is pushed.

#### Webhook flow:

```
Developer pushes code
        ↓
GitHub sends webhook event
        ↓
Jenkins triggers pipeline
```

#### Webhook Configuration (GitHub)

```
Repository → Settings → Webhooks → Add Webhook
```

#### Enter:

```
Payload URL: http://<jenkins-ip>:8080/github-webhook/
Content Type: application/json
Events: Push
```

#### Benefits of Webhooks:

* Enables real Continuous Integration (CI)

* No manual build triggers

* Faster feedback on code changes

* Prevents broken code from reaching production
