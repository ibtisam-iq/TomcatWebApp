# Tomcat Web App

## Project Overview
This project is a Java-based web application that runs on Apache Tomcat. It follows a traditional servlet-JSP model instead of a modern Spring Boot or microservices approach.

- **Backend Technology**: Java (Servlets & JSP)
- **Frontend Technology**: JSP (Java Server Pages)
- **Build Tool**: Maven (pom.xml)
- **Application Server**: Apache Tomcat
- **Folder Structure Type**: Monolithic (not fully 3-tier)

## Folder Structure Breakdown

```text
.
├── Banner.png
├── consoleOutput.txt
├── .gitignore
├── logo.png
├── pom.xml
├── projectSnapshot.png
├── README.md
└── src
    ├── main
    │   ├── java
    │   │   └── com
    │   │       └── example
    │   │           ├── HelloWorldExample.java
    │   │           └── Thing.java
    │   └── webapp
    │       ├── index.jsp
    │       └── WEB-INF
    │           └── web.xml
    └── test
        └── java
            └── com
                └── example
                    └── ThingTest.java
```

## 1️⃣ Root Files

| **File**             | **Purpose** |
|----------------------|-------------|
| `.gitignore`         | Excludes unnecessary files from Git tracking. |
| `Banner.png`, `logo.png`, `projectSnapshot.png` | Image assets (used in documentation or app UI). |
| `consoleOutput.txt`  | Likely contains runtime logs or console outputs. |
| `pom.xml`            | Maven build file – defines dependencies, plugins, and project configuration. |
| `README.md`          | Documentation explaining project setup and usage. |

## 2️⃣ Backend (Java Code)

**Path**: `src/main/java/com/example/`

| **File**                | **Purpose** |
|-------------------------|-------------|
| `HelloWorldExample.java` | Likely a servlet that handles HTTP requests and responses. |
| `Thing.java`             | A Java class (could be a model or helper utility). |

## 3️⃣ Web Application Code (JSP & Configurations)

**Path**: `src/main/webapp/`

| **File**              | **Purpose** |
|-----------------------|-------------|
| `index.jsp`           | The main frontend page (JSP is Java embedded in HTML). |
| `WEB-INF/web.xml`     | Deployment descriptor – defines servlet configurations, mappings, and security settings. |
| **JSP files**: Unlike modern frontend frameworks (React, Angular, Vue), JSP allows dynamic content rendering using Java within HTML. |
| **web.xml**: Essential for servlet-based applications, defining routing and configuration. |

## 4️⃣ Testing

**Path**: `src/test/java/com/example/`

| **File**              | **Purpose** |
|-----------------------|-------------|
| `ThingTest.java`      | Likely a unit test for `Thing.java`, verifying backend logic. |

## Analysis: Where Does This Project Fit?

| **Feature**          | **Classification**           |
|----------------------|------------------------------|
| **Architecture**      | 2-tier (Monolithic Web App)  |
| **Backend Framework** | Servlet-based (Traditional Java EE) |
| **Frontend**          | JSP (Server-rendered UI, No React/Angular) |
| **Application Server**| Tomcat (WAR deployment)      |
| **Build System**      | Maven (pom.xml for dependency management) |

## Comparison to Other Web Apps

| **Project Type**                   | **Backend**        | **Frontend** | **Architecture**    |
|-------------------------------------|--------------------|--------------|---------------------|
| React + Node.js + MySQL             | Node.js (Express)  | React        | 3-tier              |
| Spring Boot + React + MySQL         | Spring Boot        | React        | 3-tier              |
| Flask + React + PostgreSQL          | Flask              | React        | 3-tier              |
| **This Tomcat WebApp**              | Java Servlets      | JSP          | 2-tier (Monolithic) |

## Conclusion

✅ This project is a **2-tier**, **monolithic web application** running on Tomcat.  
✅ It does not follow a modern **3-tier** (frontend, backend, database) separation.  
✅ JSP and servlets are older but still used for small Java web applications.  

If you want to modernize it, you could:
- Replace JSP with **React/Vue.js**
- Replace servlets with **Spring Boot** (REST API)

## Brief Introduction

This is a simple web application built using the Tomcat server. It consists of a single servlet that handles HTTP requests and responds with a simple "Hello World!" message.

The application is deployed as a WAR file, which is a standard format for Java web applications. The WAR file is then deployed to a Tomcat server using Jenkins, where it can be accessed via a web browser.

The context path of the application is set to `/hello-world`, which means that the application can be accessed at the URL `http://localhost:8080/hello-world`.

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Installation Steps](#installation-steps)
   - [1. Download and Extract Tomcat](#1-download-and-extract-tomcat)
   - [2. Configure Tomcat Users](#2-configure-tomcat-users)
   - [3. Create Start and Stop Scripts](#3-create-start-and-stop-scripts)
   - [4. Modify Access Restrictions](#4-modify-access-restrictions)
3. [Starting and Stopping Tomcat](#starting-and-stopping-tomcat)
4. [License](#license)

## Prerequisites

- A Linux-based operating system with `sudo` privileges.
- Basic knowledge of Linux command-line operations.

## Installation Steps

### 1. Download and Extract Tomcat

1. **Switch to the root user:**

   ```bash
   sudo su
   ```

2. **Navigate to the `/opt` directory:**

   ```bash
   cd /opt
   ```

3. **Download the Apache Tomcat 9.0.65 tarball:**

   ```bash
   sudo wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.65/bin/apache-tomcat-9.0.65.tar.gz
   ```

4. **Extract the downloaded tarball:**

   ```bash
   sudo tar -xvf apache-tomcat-9.0.65.tar.gz
   ```

### 2. Configure Tomcat Users

1. **Navigate to the Tomcat configuration directory:**

   ```bash
   cd /opt/apache-tomcat-9.0.65/conf
   ```

2. **Edit the `tomcat-users.xml` file to add an admin user:**

   ```bash
   sudo vi tomcat-users.xml
   ```

3. **Add the following line before the closing `</tomcat-users>` tag:**

   ```xml
   <user username="ibtisam" password="ibtisam.1" roles="admin-gui,manager-gui,manager-script"/>
   ```

   This creates an admin user with the username `ibtisam` and the password `ibtisam.1`. The user is assigned roles that allow access to the administrative and management interfaces.

### 3. Create Start and Stop Scripts

1. **Create symbolic links for the Tomcat start and stop scripts:**

   ```bash
   sudo ln -s /opt/apache-tomcat-9.0.65/bin/startup.sh /usr/bin/startTomcat
   sudo ln -s /opt/apache-tomcat-9.0.65/bin/shutdown.sh /usr/bin/stopTomcat
   ```

   These links allow you to start and stop Tomcat using the `startTomcat` and `stopTomcat` commands from any directory.

### 4. Modify Access Restrictions

1. **Edit the `context.xml` file for the Manager web application:**

   ```bash
   sudo vi /opt/apache-tomcat-9.0.65/webapps/manager/META-INF/context.xml
   ```

2. **Comment out the `RemoteAddrValve` configuration:**

   ```xml
   <!--
   <Valve className="org.apache.catalina.valves.RemoteAddrValve"
   allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />
   -->
   ```

   This change removes the restriction that only allows access to the Manager application from localhost.

3. **Edit the `context.xml` file for the Host Manager web application:**

   ```bash
   sudo vi /opt/apache-tomcat-9.0.65/webapps/host-manager/META-INF/context.xml
   ```

4. **Comment out the `RemoteAddrValve` configuration:**

   ```xml
   <!--
   <Valve className="org.apache.catalina.valves.RemoteAddrValve"
   allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />
   -->
   ```

   This change removes the restriction that only allows access to the Host Manager application from localhost.

## Starting and Stopping Tomcat

- **To stop Tomcat:**

  ```bash
  sudo stopTomcat
  ```

- **To start Tomcat:**

  ```bash
  sudo startTomcat
  ```

These commands will control the Tomcat server's operation.

## Project Structure

Please refer to `consoleOutput.txt` for more details. 😊

## Project Snapshot
![Project Snapshot](./projectSnapshot.png)


