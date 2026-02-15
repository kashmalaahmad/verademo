**Verademo Static Code Analysis using Docker & SonarQube**

This repository contains a containerized setup of the open-source Java web application **Verademo**, along with static code analysis performed using SonarQube.

The purpose of this setup is to demonstrate how maintainability issues such as:
* Resource leaks
* Improper exception handling
* Logical errors
* Accessibility violations
* CSS compliance issues
can be automatically detected using static code analysis tools in a reproducible Dockerized environment.

## Project Overview
* **Application:** Verademo (Java Web Application)
* **Build Tool:** Maven
* **Containerization:** Docker
* **Static Analysis Tool:** SonarQube
* **Scanner:** SonarScanner CLI

The application has been containerized to ensure consistent execution across different systems and to simplify the static analysis workflow.
## Prerequisites

Make sure the following tools are installed on your system:

* Docker
* Docker Desktop (Windows/macOS)

## Running the Application in Docker

Navigate to the application directory:

```bash
cd app
```

Build the Docker image:

```bash
docker build -t verademo-app .
```

Run the container:

```bash
docker run -d -p 8080:8080 verademo-app
```

The application should now be accessible at:

```
http://localhost:8080
```

---

## Deploying SonarQube using Docker

Pull the official SonarQube image:

```bash
docker pull sonarqube
```

Run the SonarQube container:

```bash
docker run -d --name sonarqube -p 9000:9000 sonarqube
```

Access the SonarQube dashboard:

```
http://localhost:9000
```

Default login credentials:

```
Username: admin  
Password: admin
```

You will be prompted to change the password after first login.

## Running Static Code Analysis

1. Create a new project from the SonarQube dashboard
2. Generate an authentication token

Run the SonarScanner CLI:

```bash
docker run --rm \
-e SONAR_HOST_URL="http://host.docker.internal:9000" \
-e SONAR_LOGIN="your_token_here" \
-v ${PWD}:/usr/src \
sonarsource/sonar-scanner-cli \
-Dsonar.projectKey=verademo \
-Dsonar.sources=. \
-Dsonar.java.binaries=target
```

Once the analysis is complete, refresh your SonarQube dashboard to view:

* Bugs
* Code Smells
* Maintainability Issues
* Severity Distribution
* Affected Components

---

## Why Use Static Analysis?

Static analysis tools like SonarQube help in:

* Detecting hidden maintainability issues
* Preventing memory and resource leaks
* Improving code readability
* Enforcing coding standards
* Identifying accessibility problems
* Enhancing long-term software quality

## License

This repository is intended for educational and demonstration purposes.

