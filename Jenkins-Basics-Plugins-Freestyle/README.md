## 📘 Jenkins-Basics-Plugins-Freestyle


### 🔹 **1. Jenkins Dashboard**
The Jenkins Dashboard is the **main home screen** and the control center of Jenkins. From here, you manage every part of Jenkins.


#### ✔ What you can do from Dashboard:
- Create new jobs
- View all projects
- Check build history
- Manage plugins
- Configure Jenkins settings
- Manage users


#### ⭐ Interview Line:
**“The Jenkins Dashboard is the main control panel where we view and manage all Jenkins jobs and builds.”**


---


### 🔹 **2. Jenkins Plugins**
Plugins extend Jenkins' functionality. Jenkins core is minimal; plugins add features.


#### ✔ Why plugins?
- Git integration
- Maven/Gradle builds
- Pipeline support
- Docker builds
- Email notifications
- Cloud integrations


#### ⭐ Interview Line:
**“Plugins extend Jenkins functionality based on project needs.”**


---


### 🔹 **3. What is Git?**
Git is a **distributed version control system** used to track and manage source code.


#### ✔ Git helps to:
- Track changes
- Maintain history
- Work in teams
- Roll back to earlier versions
- Manage branches


#### Common Git commands:
#### ⭐ Why Git in Jenkins?
Jenkins uses Git to **pull the latest version of the code** during each build.


---


### 🔹 **4. What is GitHub?**
GitHub is a **cloud hosting platform** for Git repositories.


#### ✔ GitHub provides:
- Remote code storage
- Branch management
- PR system
- Collaboration, issues, CI triggers


#### ⭐ Interview Line:
**“Git is the version control tool; GitHub is the platform that stores Git repositories.”**


---



### 🔹 **5. What is SCM in Jenkins?**
SCM (Source Code Management) tells Jenkins **where your code lives**.


#### ✔ In Jenkins, SCM = Git Repository
Fields include:
- Repository URL
- Branch (main/master/dev)
- Credentials (for private repos)


#### ⭐ Interview Line:
**“SCM is the configuration where Jenkins fetches source code from Git/GitHub.”**


---


### 🔹 **6. What is a Freestyle Project?**
A Freestyle project is the **simplest type of Jenkins job**, used for basic builds.


#### ✔ Used for:
- Pulling code from Git
- Running shell commands
- Running Maven/Gradle
- Testing apps


#### ⭐ Interview Line:
**“Freestyle Project is a beginner-friendly Jenkins job used for simple automation without pipeline scripting.”**


---


### 🔹 **7. What is a Jenkins Build?**
A build is one **complete execution** of a Jenkins job.


#### Build includes:
- Pulling code
- Running scripts or tools
- Producing output
- Marking success or failure


Each build is identified by a number: #1, #2, #3…


#### ⭐ Interview Line:
**“A build is a single execution of a Jenkins job with logs and results.”**


---


### 🔹 **8. What is Console Output?**
Console Output is the **log file** of the build.


#### Shows:
- Commands executed
- Success or failure
- Errors
- Git branch/commit


#### ⭐ Why important?
It is the **first place to debug errors**.


---


### 🔹 **9. What is a Jenkins Workspace?**
Workspace is the directory where Jenkins downloads your repo and runs builds.


#### Contains:
- Git code
- Build artifacts
- Logs
- Temporary files


Example path on Linux:

#### ⭐ Interview Line:
**“Workspace is the local directory where Jenkins clones code and runs builds.”**


---


### 🔹 **10. How Git + Jenkins Work Together (Complete CI Flow)**


#### CI Pipeline Flow:
1. Code pushed to GitHub
2. Jenkins fetches code using Git
3. Freestyle job runs build/test
4. Logs shown in Console Output
5. Workspace stores artifacts


#### ⭐ Interview Summary:
**“Git stores the code, Jenkins pulls the code and automates the build/testing process.”**


---


## Quick start


1. Clone this repo: `git clone <repo-url>`
2. Inspect `Jenkins/job-config.xml` to see the Freestyle job configuration that points to this repository.
3. Create a new Jenkins Freestyle job and use the `config.xml` (use Jenkins UI or CLI to create).
4. Or create a pipeline job and reference the `Jenkinsfile`.


## Files
- `Jenkins/job-config.xml` — Freestyle job config you can upload to Jenkins (use `Manage Jenkins` → `Create new job` → `Import config.xml` or use Jenkis CLI).
- `scripts/build-and-test.sh` — build script run by the Freestyle job.
- `sample-app/` — small Maven app that `mvn test` will pass.
- `Jenkinsfile` — optional pipeline example for comparison.


## Notes for private GitHub repos
- Add credentials in Jenkins (`Manage Jenkins` → `Credentials`) and reference them in job config if needed.
- Alternatively, use a personal access token and add it to job configuration.
