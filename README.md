# AutoFlaskDeploy

## Overview
AutoFlaskDeploy is a CI/CD pipeline for deploying a Flask application using Jenkins, Docker, and AWS services. The pipeline automates building, pushing to AWS Elastic Container Registry (ECR), and deploying the application on an EC2 instance.

## Features
- Flask web application
- Dockerized for containerized deployment
- Jenkins pipeline for automated build and deployment
- AWS ECR for container registry
- EC2 instance for hosting the application

## Prerequisites
Before running this project, ensure you have the following installed:
- **Python 3.9+**
- **Docker**
- **Jenkins** (with required plugins: Pipeline, Amazon EC2, Docker Pipeline)
- **AWS CLI** (configured with appropriate credentials)
- **Git**

## Project Structure
```
flask_with_jenkins/
│── Dockerfile           # Defines the container image
│── Jenkinsfile          # Jenkins pipeline configuration
│── README.md            # Project documentation
│── app.py               # Flask application code
│── requirements.txt     # Python dependencies
```

## Setup Instructions

### 1. Clone the Repository
```sh
git clone https://github.com/Neta-Aviv/AutoFlaskDeploy.git
cd AutoFlaskDeploy
```

### 2. Install Dependencies
```sh
pip install -r requirements.txt
```

### 3. Run Locally (Optional)
```sh
python app.py
```
Access the app at `http://localhost:5000`

### 4. Build and Push Docker Image (Manually)
```sh
docker build -t neta/flaskapp:latest .
docker tag neta/flaskapp:latest 767828746131.dkr.ecr.us-east-1.amazonaws.com/neta/flaskapp:latest
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 767828746131.dkr.ecr.us-east-1.amazonaws.com

docker push 767828746131.dkr.ecr.us-east-1.amazonaws.com/neta/flaskapp:latest
```

### 5. Deploy Using Jenkins
1. Set up Jenkins and configure AWS credentials.
2. Add the repository as a Jenkins pipeline project.
3. Ensure the Jenkins server has access to Docker and AWS CLI.
4. Run the pipeline to build, push, and deploy the Flask app.

### 6. Verify Deployment
```sh
curl http://<EC2_INSTANCE_PUBLIC_IP>:5000
```
It should return `Hello, World!`

## Future Improvements
- Add unit tests
- Implement Blue-Green or Canary deployment strategy
- Enhance security best practices for AWS credentials
