# BUILDING OUR FIRST FREESTYLE PROJECT INSIDE JENKINS

# 🟩 STEP 1 – INSTALL REQUIRED PLUGINS

Go to: Manage Jenkins → Plugins → Available


Search & install:

- ✅ Git Plugin  
- ✅ GitHub Plugin  
- ✅ Maven Integration Plugin  
- ✅ Pipeline Plugin  
- ✅ Email Extension Plugin  

After installation → Restart Jenkins if required.

👉 **Plugins extend Jenkins functionality.**

---

# 🟨 STEP 2 – INSTALL GIT ON AWS EC2 (IMPORTANT)

Login to your EC2 server:

```bash
ssh -i jenkins-key.pem ubuntu@<EC2-PUBLIC-IP>
```
Install Git:
```bash
sudo apt update
sudo apt install git -y
```
Verify:
```bash
git --version
```
Git must be installed for Jenkins to clone GitHub repositories.

# 🟧 STEP 3 – CONFIGURE GIT IN JENKINS
```bash
Manage Jenkins → Tools
```

### Find the Git section:

* Name → Default-Git

* Path to Git → Leave empty (Jenkins auto-detects /usr/bin/git)

Click Save.

# 🟦 STEP 4 – CREATE A SAMPLE GITHUB REPOSITORY

On GitHub:

1. Click New Repository

2. Name → jenkins-demo

3. Keep it Public

4. Check → Add README

5. Click Create Repository

Copy the repository URL:
```bash
https://github.com/username/jenkins-demo.git
```

This repo will be used by Jenkins.

# 🟩 STEP 5 – CREATE YOUR FIRST FREESTYLE PROJECT

Go to Jenkins Dashboard → Click New Item

🔹 Enter Job Name:

```bash
freestyle-demo
```

Select:
```bash
Freestyle Project
```

Click OK

### 🔸 A) CONFIGURE SOURCE CODE MANAGEMENT (SCM)

Under Source Code Management:

Select Git

Enter repository URL:
```bash
https://github.com/username/jenkins-demo.git
```

Branch:
```bash
main
```

👉 Jenkins will now pull code from GitHub.


### 🔸 B) ADD BUILD STEPS

Scroll to Build section.

Click:
```bash
Add Build Step → Execute Shell
```

Paste:
```bash
echo "Hello from Jenkins Freestyle Project"
ls -l
```

This will print a message + list files in Jenkins workspace.

### 🔸 C) SAVE THE JOB

Click Save ✔

Your job is now ready to run.


# 🟥 STEP 6 – RUN YOUR FIRST JENKINS BUILD

Inside your job:

Click:
```bash
Build Now
```

A new build appears in the left panel:
```bash
#1
```

Click:
```bash
#1 → Console Output
```

You should see:
```bash
Hello from Jenkins Freestyle Project
```

🎉 Your first Jenkins automation is successful!

# 🟪 STEP 7 – UNDERSTANDING CONSOLE OUTPUT

The Console Output shows:

* Git clone process

* Workspace path

* Your shell script output

* Success/Failure

This is the most important page for debugging Jenkins jobs.
