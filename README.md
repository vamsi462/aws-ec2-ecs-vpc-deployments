# Serverless Two-Tier Web Application on AWS

This project demonstrates the containerization and deployment of a two-tier web application (Node.js/Express frontend and Python/Flask backend) using a fully serverless AWS architecture. 

## 🏗️ Architecture Stack
* **Frontend:** Node.js & Express.js (Port 3000)
* **Backend:** Python & Flask (Port 5000)
* **Containerization:** Docker
* **Image Registry:** Amazon Elastic Container Registry (ECR)
* **Orchestration & Compute:** Amazon Elastic Container Service (ECS) on AWS Fargate
* **Networking & Security:** Custom AWS Virtual Private Cloud (VPC) with isolated Security Groups

## 🚀 Deployment Workflow
1. **Containerization:** Both the frontend and backend applications were individually containerized using Docker.
2. **Registry Push:** Docker images were authenticated and pushed to private Amazon ECR repositories using the AWS CLI.
3. **Custom Networking:** A custom AWS VPC was provisioned with public subnets and an Internet Gateway to handle external traffic routing.
4. **Task Definitions:** ECS Task Definitions were authored for both tiers, mapping specific vCPU/Memory allocations and injecting dynamic environment variables (e.g., passing the Backend IP to the Frontend container).
5. **Serverless Execution:** The containers were deployed as standalone tasks on AWS Fargate, eliminating the need to provision or manage underlying EC2 instances. 
6. **Security:** Network traffic was strictly controlled using VPC Security Groups, ensuring the principle of least privilege by only exposing ports 3000 and 5000.

## 🔄 Traffic Flow
1. A client accesses the Express frontend via the Fargate task's Public IPv4 address on port 3000.
2. Upon form submission, the frontend Node.js application initiates a POST request.
3. The request is routed internally over the custom VPC to the Flask backend's Public IP on port 5000.
4. The Flask container processes the payload and returns a success response back to the frontend UI.
