# 📘 Maven

This module explains **Apache Maven**, its role in Java projects, and how it integrates with Jenkins for Continuous Integration (CI).

---

## 🔹 1️⃣ What is Maven?

**Apache Maven** is a **build automation and dependency management tool** used mainly for **Java projects**.

Maven helps developers automate tasks that are usually done manually during application development.

### Maven is used to:
- Automatically download required libraries (dependencies)
- Compile Java source code
- Run unit tests
- Package applications into `.jar` or `.war` files
- Maintain a standard project structure

👉 **Jenkins uses Maven to build Java applications automatically.**

---

## 🔹 2️⃣ What is a Maven Project?



A **Maven Project** is a Java project that follows a **standard directory structure** and is controlled by a file called `pom.xml`.

### Standard Maven Project Structure:
```
project-name/
│
├── pom.xml
└── src
├── main
│ └── java
│ └── Application source code
│
└── test
└── java
└── Unit test cases


```

### Why this structure is important:
- All Maven tools expect this format
- Jenkins and CI tools understand it automatically
- Makes projects easy to maintain and understand

---

## 🔹 3️⃣ What is `pom.xml`?

`pom.xml` stands for **Project Object Model**.

It is the **core configuration file** of a Maven project.

### `pom.xml` defines:
- Project name (`artifactId`)
- Organization (`groupId`)
- Project version
- Java version
- Dependencies (external libraries)
- Build instructions and plugins

Without `pom.xml`, Maven cannot build the project.

---

## 🔹 4️⃣ Maven Build Lifecycle

Maven uses a **build lifecycle**, which is a sequence of predefined phases executed in order.

### Maven Lifecycle Phases:

| Phase     | Description |
|----------|------------|
| validate | Checks project structure and configuration |
| compile  | Compiles `.java` files into `.class` files |
| test     | Runs unit test cases |
| package  | Creates `.jar` or `.war` file |
| verify   | Performs quality checks |
| install  | Stores the package in local Maven repository |
| deploy   | Uploads the package to a remote repository |

---

### 📌 Most Common Maven Command

```bash
mvn clean install
```

This command executes:
```bash
clean → validate → compile → test → package → install
```

### Local Maven Repository:

Maven stores downloaded dependencies locally at:

```
~/.m2/repository

```

This improves build speed by avoiding repeated downloads.

## 🔹 5️⃣ Why Jenkins + Maven Together?

* Jenkins is an automation server

* Maven is a build tool

Together, they enable Continuous Integration (CI).

### Jenkins + Maven Workflow:
```bash
Developer pushes code
        ↓
Jenkins detects changes
        ↓
Jenkins runs Maven build
        ↓
Maven compiles, tests, packages
        ↓
Jenkins reports build status

```

This ensures:

* Automated builds

* Automated testing

* Early bug detection

## 🔹 6️⃣ Manual Build vs Jenkins Build

| Feature     | Manual Build            | Jenkins Build           |
| ----------- | ----------------------- | ----------------------- |
| Trigger     | Developer runs commands | Automatically triggered |
| Speed       | Slow                    | Fast                    |
| Testing     | Often skipped           | Always executed         |
| Errors      | Human errors possible   | Reliable & consistent   |
| Scalability | Poor                    | High                    |

### Why companies avoid manual builds:

* Inconsistent results

* Human mistakes

* Time consuming

### Why companies use Jenkins builds:

* Fully automated

* Repeatable and reliable

* Scalable for teams
