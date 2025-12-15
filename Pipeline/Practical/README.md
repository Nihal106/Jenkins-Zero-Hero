# 💻 Jenkins Pipelines (Practical)

This practical demonstrates how to create and run a **Jenkins Pipeline** using a `Jenkinsfile` stored in a GitHub repository.  
You will move from manual Freestyle jobs to **Pipeline as Code**, which is the industry standard for CI/CD.


## 🛠 Prerequisites

- Jenkins installed and running
- GitHub repository with Maven project
- Maven configured in Jenkins
- AWS EC2 instance (for agent – optional)
- Git installed

---

## ✅ STEP 1 – Create Jenkinsfile in Repository

1. Open your GitHub repository.
2. In the **root directory**, create a file named:
   'Jenkinsfile'

   
3. Paste a **Declarative Pipeline** example inside the file:

```groovy
// Jenkinsfile (Declarative) — use checkout scm to avoid branch mismatches
pipeline {
  // Prevent concurrent builds and avoid resume after restart (optional policies)
  options {
    disableConcurrentBuilds()
    skipDefaultCheckout()     // we'll explicitly use checkout scm in the Checkout stage
    // you can add buildDiscarder(logRotator(...)) here if desired
  }

  agent any
  stages {
    stage('Checkout') {
      steps {
        // Use the SCM already configured for the job (Pipeline from SCM)
         checkout scm
        // If you prefer explicit git with branch:
        // git branch: 'main', url: 'https://github.com/Nihal106/jenkins-demo.git'
      }
    }

    stage('Build') {
      steps {
        echo 'Building...'
        // Use Maven if your project uses Maven. Adjust if using gradle/npm etc.
        sh 'mvn -B clean package'
      }
    }

    stage('Test') {
      steps {
        echo 'Running tests...'
        sh 'mvn -B test'
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
    always {
      // useful cleanup/diagnostics: list workspace
      sh 'echo "Workspace contents:"; ls -la || true'
    }
  }
}
```
4. Commit and push the file to GitHub.

#### 📌 This enables Pipeline as Code.

## ✅ STEP 2 – Create Pipeline Job in Jenkins

#### 1. Open Jenkins Dashboard

#### 2. Click New Item

#### 3. Enter job name:
```
pipeline-demo
```

#### 4. Select Pipeline → Click OK

### 🔹 Pipeline Configuration

#### Configure the job as follows:

#### * Definition: Pipeline from SCM

#### * SCM: Git

#### * Repository URL:
```
https://github.com/yourname/jenkins-maven-demo.git
```

#### * Branch: main

#### * Script Path: Jenkinsfile

#### Click Save ✅

#### 📌 Jenkins will now always read the pipeline steps from GitHub.

## ✅ STEP 3 – Run the Pipeline

#### 1. Click Build Now

#### 2. Open:
```
Build #1 → Console Output
```

### Expected Output:
```
Checking out Git repository
Building...
Running tests...
BUILD SUCCESS
```

#### 📌 This confirms that:

* Jenkinsfile is valid

* GitHub integration works

* Pipeline stages executed successfully


## ✅ STEP 4 – Add Agent Node (Optional)

#### This step runs pipeline jobs on a remote EC2 agent instead of the Jenkins controller.

### 🔹 Steps:

#### 1. Jenkins Dashboard → Manage Jenkins

#### 2. Go to Nodes and Clouds

#### 3. Click New Node

#### 4. Enter:
```
Name: aws-node
```

#### 5. Select:
```
Permanent Agent
```
#### 6. Configure:

* Remote root directory: /home/ubuntu/jenkins
  
* Give a Label
  ```
  aws-node
  ```

  #### This is the Label which we give in the Jenkinsfile.
  
* Launch method: SSH

* Host: Give Your Public IP of the EC2.

* In Credentials Create a new Credential: 

   * Kind: SSH Username with Private Key.
 
   * Scope: Global
 
   * Give any ID and Description
 
   * Username:  should be the username in the server by default for ubuntu server is 'ubuntu'.
 
   * Private Key: Enter Directly -> Add -> Paste your keypair of the server
 
 * Host Key Verification Strategy: Manually Trusted Key Verification Strategy.
 
 * Enable the Disk Space Monitoring Threshold and Lower Everything otherwise you have to choose a higher spec server.
 
 * Then Save and connect the node.

 * Make sure Your server have git and maven installed.

 * Update Jenkinsfile to Use Agent:

```
pipeline {
    agent { label 'aws-node' }
    ...
}
 ```
#### 📌 The pipeline will now run on the EC2 agent instead of the Jenkins controller.

## ✅ STEP 5 – GitHub Webhook Test

#### This step enables automatic pipeline execution.

### 🔹What to do:

#### 1. Push any change to the GitHub repository.

#### 2. Jenkins pipeline should start automatically.

#### 📌 This confirms webhook integration is working.


#### 🔁 How Webhook Works
```
Developer pushes code
        ↓
GitHub sends webhook event
        ↓
Jenkins receives event
        ↓
Pipeline starts automatically

```

### Steps to Configure Webhook in Github:

#### 1. Open your GitHub repository

#### 2. Go to:
```
Settings → Webhooks → Add webhook
```

#### 3. Enter the following details:

#### * Payload URL:
```
http://<jenkins-public-ip>:8080/github-webhook/
```

#### * Content type:
```
application/json
```

#### * Which events would you like to trigger this webhook?
```
Just the push event
```

#### 4. Click Add Webhook

#### 📌 GitHub will send a test request.
You should see ✔ Delivered.


### Steps to Configure Webhook in Jenkins:

#### 1. Open your pipeline job

#### 2. Click Configure

#### 3. Scroll to Build Triggers

#### 4. Enable:
```
GitHub hook trigger for GITScm polling
```

#### 5. Click Save


### Test Webhook: 

#### 1. Make a small change in your repository (edit README, add comment, etc.)

#### 2. Commit and push.

### Expected Result:

#### * Jenkins pipeline starts automatically
#### * No manual Build Now click required

#### 📌 This confirms webhook integration is working.
