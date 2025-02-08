# AWS-ECR
AWS Elastic Container Registry (How to push Docker Image to AWS-ECR "Private & Public ECR")
## How to push Docker Image to Amazon Elastic Container Registry "PRIVATE REPOSITORY"(AWS ECS)
### Docker and AWS ECR Integration to push an image to a PRIVATE REPOSITORY(AWS ECS).
This documentation covers the steps to integrate Docker with AWS Elastic Container Registry (ECR) for storing and pushing container images.

## 1 Setup and Commands
### 1.1. Configure AWS CLI
```bash
aws configure
```
- *Explanation:* This command configures the AWS CLI by prompting you to enter your AWS credentials (Access Key ID, Secret Access Key, region, and output format). This ensures that your local environment is set up for interacting with AWS services.
### 1.2. Log into AWS ECR with Docker
```bash
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin <aws account_id Number.>.dkr.ecr.ap-south-1.amazonaws.com
```
- *Explanation:* This command retrieves an authentication token for logging into AWS ECR and then pipes the token into `docker login`. It authenticates Docker to interact with the ECR registry (in this case, the `ap-south-1` region). The `--password-stdin` option securely passes the password to Docker.
### 1.3. Create ECR Repository for "hello-repository" through AWS CLI

```bash
aws ecr create-repository --repository-name hello-repository --region ap-south-1
```
- *Explanation:* This command creates a new ECR repository named `hello-repository` in the `ap-south-1` region.

### 1.4. List Local Docker Images & Tag Local Docker Image for ECR
```bash
docker images
docker tag hello-world:latest 339713104321.dkr.ecr.ap-south-1.amazonaws.com/hello-repository
```
- *Explanation:* This command tags the local `hello-world:latest` Docker image with the full ECR repository URL (`339713104321.dkr.ecr.ap-south-1.amazonaws.com/hello-repository`) to prepare it for pushing to the repository.

### 1.5. Push Docker Image to ECR
```bash
docker push 339713104321.dkr.ecr.ap-south-1.amazonaws.com/hello-repository:latest
```
- *Explanation:* This command pushes the tagged Docker image (`hello-world:latest`) to the specified repository (`hello-repository`) on AWS ECR.


## 2. Setup and Commands
### 2.1. Configure AWS CLI
```bash
aws configure
```
- *Explanation:* This command configures the AWS CLI by prompting you to enter your AWS credentials (Access Key ID, Secret Access Key, region, and output format). This ensures that your local environment is set up for interacting with AWS services.
### 2.2. Log into AWS ECR with Docker
```bash
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin <aws account_id Number.>.dkr.ecr.ap-south-1.amazonaws.com
```
### 2.3. Create ECR Repository for "hello-repository" in ECR AWS Console
- Create a Repo in Amazon Elastic Container Registry and Copy the 

### 2.4 Tag Apache Tomcat Docker Image for ECR
```bash
docker tag apache-tomcat:latest 339713104321.dkr.ecr.ap-south-1.amazonaws.com/apache-tomcat
```
- *Explanation:* This command tags the `apache-tomcat:latest` Docker image with the ECR repository URL (`339713104321.dkr.ecr.ap-south-1.amazonaws.com/apache-tomcat`).

### 2.5 Push Apache Tomcat Docker Image to ECR
```bash
docker push 339713104321.dkr.ecr.ap-south-1.amazonaws.com/apache-tomcat:latest
```
- Explanation: This command pushes the `apache-tomcat:latest` image to the `apache-tomcat` repository in AWS ECR.
---
# Docker and AWS ECR Integration to push an image to a PUBLIC REPOSITORY(AWS ECS).
## How to push Docker Image to Amazon Elastic Container Registry "PUBLIC REPOSITORY"(AWS ECS)
### AWS CLI and Docker Integration for Public ECR

This repository contains a guide for configuring AWS CLI, integrating it with Docker, and authenticating with Amazon Elastic Container Registry (ECR) Public.

## Prerequisites
1. **AWS CLI Version 2**: Ensure you have AWS CLI version 2 installed. Follow the instructions in this guide to install or upgrade.
2. **Docker**: Ensure Docker is installed and running on your system.
3. **Network Access**: Verify connectivity to AWS public endpoints.

## Installation and Configuration

### 1. Download and Install AWS CLI Version 2
- **Run the following commands to download and install AWS CLI v2 on a Linux system:**
```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```
- **Verify the installation:**
```bash
/usr/local/bin/aws --version
```
### 2. Remove Previous AWS CLI Versions
- **If AWS CLI v1 is installed, remove it to avoid conflicts:**
  ```bash
  sudo yum remove aws-cli -y
  ```
- **Update the system `PATH` to ensure AWS CLI v2 is prioritized:**
  ```bash
  export PATH=/usr/local/bin:$PATH
  ```
- **Make the change permanent:**
  ```bash
  echo 'export PATH=/usr/local/bin:$PATH' >> ~/.bashrc
  source ~/.bashrc
  ```
### 3. Configure AWS CLI
- **Run the configuration command to set up AWS credentials and default region:**
  ```bash
  aws configure
  ```
  - This command prompts for:
    - AWS Access Key ID
    - AWS Secret Access Key
    - Default Region Name (e.g., us-east-1 for public ECR)
    - Default Output Format (e.g., json)

### 4. Docker Login to Amazon ECR Public
- **Authenticate with Public ECR**
  - Run the following command to authenticate Docker with Amazon ECR Public:
    ```bash
    aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws
    ```
### 5. Testing Connectivity
- **Verify connectivity to Amazon ECR Public endpoints:**
  ```bash
  curl https://api.ecr-public.us-east-1.amazonaws.com/
  ```
### 6. Docker Login with Manual Authentication
- **You can also manually log in to Docker using an authentication token provided by AWS CLI.**
```bash
aws ecr-public get-login-password --region us-east-1
```
- **Copy the output password and use it to log in:**
```bash
docker login --username AWS --password <copied-password> public.ecr.aws
```
**Explanation**:
- Replace `<your-authentication-token>` with the token obtained from `aws ecr-public get-login-password`.
- This logs Docker into the public Amazon Elastic Container Registry.

### 7. Verify Docker Images
List all the Docker images currently available on your system:
```bash
docker images
```

### 8. Tagging a Docker Image for Public ECR
- **Tag an existing local Docker image to prepare it for pushing to Amazon ECR Public:
**
```bash
docker tag <source-image>:<tag> public.ecr.aws/<your-repository>/<image-name>:<tag>
```
Example:
```bash
docker tag mallick17/webap:latest public.ecr.aws/w9f8l1p1/mallick17/webap:latest
```
**Explanation**:
- `<source-image>`: Name of the local image.
- `<tag>`: The tag you want to assign (e.g., `latest`).
- `<your-repository>`: Your public ECR repository path.
- `<image-name>`: The name of the image to push.

### 9. Pushing the Image to Amazon ECR Public
Push the tagged Docker image to Amazon ECR Public:

```bash
docker push public.ecr.aws/<your-repository>/<image-name>:<tag>
```
Example:
```bash
docker push public.ecr.aws/w9f8l1p1/mallick17/webap:latest
```
**Explanation**:
- Uploads the Docker image to the specified repository in Amazon ECR Public.










