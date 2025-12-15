# 💻 Jenkins + Maven (Practical)

This practical demonstrates how to **build a real Java application automatically using Jenkins and Maven**.  
By the end of this lab, Jenkins will generate a `.jar` file without running Maven manually.

## 🛠 Prerequisites

- Jenkins installed and running
- AWS EC2 (Ubuntu)
- GitHub account
- Java 17 installed

---

## ✅ STEP 1 – Install Maven on AWS EC2

Login to your EC2 instance and run:

```bash
sudo apt update
sudo apt install maven -y
```

Verify Maven installation:

```bash
mvn -version
```

If Maven version is displayed, installation is successful ✅

## ✅ STEP 2 – Configure Maven in Jenkins

#### 1. Go to Jenkins Dashboard

#### 2. Navigate to:
```bash
Manage Jenkins → Tools
```

#### 3. Scroll to Maven

#### 4. Add Maven configuration:

* Name: Maven-3

* ✅ Install automatically

* Version: Latest

#### 5. Click Save

📌 Jenkins will now manage Maven centrally for all jobs.

## ✅ STEP 3 – Create a Sample Java Maven Project on GitHub
### 🔹 Create GitHub Repository

#### Create a new repository:

```bash
jenkins-maven-demo
```

#### 🔹 Clone Repository on EC2
```
git clone https://github.com/yourname/jenkins-maven-demo.git
cd jenkins-maven-demo
```
#### 🔹 Create Maven Directory Structure
```
mkdir -p src/main/java
mkdir -p src/test/java
```

#### 🔹 Create Java Application
```
nano src/main/java/App.java
```

#### Paste:
```
public class App {
    public static void main(String[] args) {
        System.out.println("Hello from Jenkins Maven Build!");
    }
}
```
#### 🔹 Create pom.xml
```
nano pom.xml
```

#### Paste:
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
         http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

    <groupId>com.jenkins</groupId>
    <artifactId>demo</artifactId>
    <version>1.0</version>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

</project>
```

#### 🔹 Commit and Push Code
```
git add .
git commit -m "add maven java project"
git push origin main
```

#### Now the project is ready for Jenkins to build.


## ✅ STEP 4 – Create a Maven Freestyle Job in Jenkins

#### 1. Jenkins Dashboard → New Item

#### 2. Job name:
```
freestyle-maven-build
```

#### 3. Select Freestyle Project → Click OK


### 🔹 Source Code Management

#### * Select Git

#### * Repository URL:
```
https://github.com/yourname/jenkins-maven-demo.git
```

#### * Branch:
```
main
```
### 🔹 Build Configuration

#### 1. Click Add Build Step

#### 2. Select:
```
Invoke Top-Level Maven Targets
```

#### 3. Configure:

* Maven Version: Maven-3

* Goals: clean package

#### 5. Click Save

## ✅ STEP 5 – Run the Build

#### 1. Click Build Now

#### 2. Open:
```
Build #1 → Console Output
```

#### You should see:
```
BUILD SUCCESS
```

### 🔹 Verify Build Artifact

#### Go to Jenkins job → Workspace → target/

#### You will find:
```
demo-1.0.jar
```

#### 🎉 Your Java application has been built automatically by Jenkins!
