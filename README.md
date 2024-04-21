# SonarQube Integration Guide

## Introduction

SonarQube is an automated code review tool that detects bugs, vulnerabilities, and code smells in your code. It can
integrate with Maven and Gradle projects to continuously inspect code quality.

## Prerequisites

- SonarQube running in a Docker container.
- Java project using Maven or Gradle.
- Docker and Docker Compose installed if using SonarQube in Docker.

## Docker Setup

If you have not already set up SonarQube in Docker, refer to the
official [SonarQube Docker images](https://hub.docker.com/_/sonarqube/) for detailed setup instructions.

## SonarQube Credentials

- **Default Username:** admin
- **Default Password:** admin

You will be prompted to change the default password on your first login.

## Maven Integration

### 1. Add SonarQube Plugin

Edit your `pom.xml` and add the SonarQube scanner plugin in the `<build><plugins>` section:

```xml

<plugin>
    <groupId>org.sonarsource.scanner.maven</groupId>
    <artifactId>sonar-maven-plugin</artifactId>
    <version>3.9.0.2155</version>
</plugin>
```

### 2. Configure SonarQube Properties

- Set the SonarQube properties in your `pom.xml` within the `<properties>` section:

```xml

<sonar.projectKey>myproject-key</sonar.projectKey>
<sonar.host.url>http://localhost:9000</sonar.host.url>
<sonar.login>the-generated-token</sonar.login>
```

### 2. Run SonarQube Analysis

- Execute the following command from your project root directory:

```bash
  Copy code
  
  mvn clean verify sonar:sonar
  Gradle Integration
```

#### 1. Apply SonarQube Plugin

- Add the SonarQube plugin to your build.gradle:

```bash
Copy code

plugins {
  id "org.sonarqube" version "3.3"
}
```

#### 2. Configure SonarQube

Set the necessary properties in your build.gradle:

```bash
Copy code
sonarqube {
  properties {
    property "sonar.projectKey", "myproject-key"
    property "sonar.host.url", "http://localhost:9000"
    property "sonar.login", "the-generated-token"
    }
}
```

#### 3. Run SonarQube Analysis

### Execute the analysis with Gradle:

```bash
Copy code
./gradlew clean build sonarqube
```

### Viewing the Analysis Results

After running the analysis, you can view the results by accessing the SonarQube dashboard at http://localhost:9000.

Further Configuration
To configure advanced SonarQube settings, refer to the SonarQube documentation.
Adjust the sonar.host.url if your SonarQube server is not running locally.
Replace the-generated-token with your actual SonarQube user token, which you can generate from the SonarQube dashboard.

This README is ready for you to use in your project, detailing how to configure and run SonarQube analysis for Maven and
Gradle projects. You can copy the code snippets and paste them into your project's README.md file.