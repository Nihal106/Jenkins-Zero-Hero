# INSTALLING JENKINS IN A AWS EC2 SERVER

# 🟦 STEP 1 — CREATE AWS EC2 SERVER

### 1️⃣ Login to AWS → Search for **EC2**
### 2️⃣ Click **Launch Instance**
### 3️⃣ Choose AMI: Ubuntu Server 22.04 LTS
### 4️⃣ Choose Instance Type: t2.micro (Free Tier Eligible)
### 5️⃣ Create a Key Pair:
- Name: **jenkins-key.pem**
- Download and keep it safely

### 6️⃣ Configure Security Group:
Allow these inbound rules:

| Port | Purpose |
|------|---------|
| **22** | SSH login |
| **8080** | Jenkins Web UI |

Source (for training): 0.0.0.0/0

### 7️⃣ Click **Launch Instance**

🎉 Your EC2 server is now created.

---

# 🟩 STEP 2 — CONNECT TO EC2 USING SSH

Go to your `.pem` file location and run:

### ✔ Fix key permissions:
```bash
chmod 400 jenkins-key.pem
```
### ✔ Connect to the server:
```bash
ssh -i jenkins-key.pem ubuntu@<EC2-PUBLIC-IP>

```
# 🟨 STEP 3 — INSTALL JAVA (REQUIRED FOR JENKINS)

### ✔ Update your apt
```bash
apt update
```
### ✔ Install Java 17:
```bash
sudo apt install -y openjdk-17-jdk

```
### ✔ Verify installation:
```bash
java -version
```

### ✔ Expected:
```nginx
openjdk version "17..."
```

# 🟧 STEP 4 — INSTALL JENKINS

### ✔ Add Jenkins GPG key:
```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

```

### ✔ Add Jenkins repository:
```bash
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

```
### ✔ Update and install Jenkins:
```bash
sudo apt update
sudo apt install -y jenkins
```

### ✔ Start Jenkins service:
```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

### ✔ Check Jenkins status:
```bash
sudo systemctl status jenkins
```
### Look for:
```arduino
active (running)
```

# 🟦 STEP 5 — OPEN JENKINS IN BROWSER

### Open:
```bash
http://<EC2-PUBLIC-IP>:8080
```

#### You will see:
```bash
Unlock Jenkins
```
### ✔ Get initial admin password:
```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Copy → Paste into the browser → Continue.

# 🟩 STEP 6 — JENKINS FIRST-TIME SETUP

### ✔ Choose:
```bash
Install Suggested Plugins
```

### It will install:

* Git plugin

* Pipeline plugin

* Credentials plugin

* UI plugins

### ✔ Create Admin User:

Fill:

* Username

* Password

* Full Name

* Email

Click Save & Finish

Click Start Using Jenkins

🎉 Jenkins Dashboard will appear.

# 🟪 STEP 7 — VERIFY JENKINS INSTALLATION

### You should now see:

* Dashboard

* New Item

* Manage Jenkins

* Build History

If yes → Jenkins is successfully installed.
