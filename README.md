# Jenkins Maven Tomcat CI/CD Pipeline

This project demonstrates a Continuous Integration/Continuous Deployment (CI/CD) pipeline for a Java-based web application hosted on an Apache Tomcat server, built using Maven, and managed by Jenkins. The project also includes a MySQL database that runs in a Docker container, managed via Docker Compose.

## Table of Contents
- [Overview](#overview)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Setup](#setup)
- [Jenkins Pipeline](#jenkins-pipeline)
- [Running the Application](#running-the-application)
- [Working of the application](#working-of-the-application)

## Overview

The main components of this project include:
- **Java Application**: A sample Java web application.
- **Apache Tomcat**: The application server where the Java application is deployed.
- **Maven**: Used for building the Java application.
- **Jenkins**: Manages the CI/CD pipeline.
- **MySQL**: A relational database, running in a Docker container.
- **Docker Compose**: Orchestrates the MySQL container.

## Architecture

![Architecture Diagram](architecture-diagram.png)

1. **Build**: Maven is used to build the Java application.
2. **Deploy**: The application is deployed to the Tomcat server.
3. **Database**: MySQL runs as a Docker container, with all necessary configurations handled by Docker Compose.
4. **CI/CD**: Jenkins manages the build, test, and deployment processes.

## Prerequisites

Ensure that you have the following installed on your local machine:
- **JDK** (Java Development Kit) 8 or higher
- **Maven** 3.6.0 or higher
- **Docker** 20.10.0 or higher
- **Docker Compose** 1.27.0 or higher
- **Jenkins** 2.235.1 or higher
- **Git**

## Jenkins Pipeline

The Jenkins pipeline defined in the Jenkinsfile consists of the following stages:

**Application Deployment:**

- Agent: The application labeled agent is used for this stage.
- Steps:
  1. Removes any existing files in the workspace.
  2. Clones the latest code from the GitHub repository: java-maven-jenkins-ci-cd.
  3. Builds a Docker image named tomcat from the Dockerfile in the repository.
  4. Runs a Docker container named tomcat-server from the tomcat image, exposing port 8080.
  5. Copies the Mumbai.pem key file to the current workspace.
  6. Uses scp to securely copy the init-scripts directory and docker-compose.yml file to a remote server at 10.0.140.175 using the Mumbai.pem SSH key.

**Database Deployment:**

- Agent: The database labeled agent is used for this stage.
- Steps:
  1. Navigates to the /home/ubuntu/ directory on the remote server.
  2. Uses Docker Compose to build and start the services defined in the docker-compose.yml file, including the MySQL database.

## Running the Application

After deploying, access the application by navigating to: http://localhost:8080/

## Working of the application
This project will start two containers - web_1 and database_1
1. web_1: This is the container which runs applicaiton frontend and backend.
2. database_1: This is the container which maintains applicaiton database.
