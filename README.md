Here’s the updated README with the new information included:

---

# React-SpringBoot-CRUD-App

This repository hosts a CRUD application built with React for the frontend and Spring Boot for the backend. The application is hosted using Nginx, showcasing skills in continuous integration and continuous deployment (CI/CD) with Jenkins.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Architecture](#architecture)
- [CI/CD Pipeline](#cicd-pipeline)
- [Setup and Installation](#setup-and-installation)
- [Usage](#usage)
- [License](#license)

## Overview

The `react-springboot-crud-app` is a CRUD (Create, Read, Update, Delete) application integrating a modern frontend built with React and a backend API developed using Spring Boot. The project emphasizes simplicity and effectiveness in CI/CD practices.

## Features

- **Frontend:** A responsive user interface built with React, providing an intuitive user experience for managing CRUD operations.
- **Backend:** A robust API built with Spring Boot, handling data persistence and business logic.
- **Web Server:** Frontend served through Nginx.
- **Database:** PostgreSQL configured for backend data storage.
- **CI/CD Pipeline:** Automated building and deployment using Jenkins.

## Technologies Used

- **Frontend:** React, HTML, CSS, JavaScript
- **Backend:** Spring Boot, Java, PostgreSQL
- **Web Server:** Nginx
- **CI/CD:** Jenkins

## Architecture

The application follows a traditional client-server architecture. The frontend and backend are coupled through RESTful API calls. The frontend is hosted using Nginx, and the backend API is deployed on a server running Spring Boot with PostgreSQL as the database.

## CI/CD Pipeline

The CI/CD pipeline for this application is configured in Jenkins, automating the following stages:

1. **Checkout Code:** The latest code from the GitHub repository is checked out.
2. **Build:** The backend API and frontend application are built.
3. **Deploy:** The application is deployed with Nginx for the frontend and a Spring Boot server for the backend.

This pipeline ensures consistent building and deployment, enhancing efficiency and reliability.

## Setup and Installation

### Prerequisites

- Jenkins server set up for CI/CD
- Nginx installed and configured to host the frontend
- Java, Maven, and PostgreSQL installed on the backend server

### Installation

1. **Clone the Repository:**

   ```bash
   git clone https://github.com/EsraaShaabanElsayed/react-springboot-crud-app.git
   ```

2. **Jenkins Pipeline Setup:**

   - Ensure Jenkins is configured to trigger on changes to the repository.
   - The pipeline script will automatically build and deploy the application.

3. **Nginx Configuration:**

   - Configure Nginx to serve the frontend application.
   - Ensure Nginx is set to listen on the desired port and points to the frontend build directory.

4. **PostgreSQL Configuration:**

   - Set up PostgreSQL for backend data storage.
   - Ensure the Spring Boot application is configured to connect to the PostgreSQL database.

---

This update includes the PostgreSQL configuration and provides a clear overview of the setup and deployment process.
