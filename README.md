# AWS-ECR
AWS Elastic Container Registry
# Docker and AWS ECR Integration to push an image to a PRIVATE REPOSITORY(AWS ECS).
## How to push Docker Image to Amazon Elastic Container Registry <PRIVATE REPOSITORY>(AWS ECS)
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
## How to push Docker Image to Amazon Elastic Container Registry <PUBLIC REPOSITORY>(AWS ECS)
