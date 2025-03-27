# Deploy a Dynamic Web App on AWS using CI/CD Pipelines with GitHub Actions

![Alt text](Diagram.png)
![Alt text](Diagram_2.png)

---
# Project Overview

This project demonstrates the deployment of a dynamic web application on AWS using CI/CD pipelines and GitHub Actions. The infrastructure is provisioned using Terraform, and the application is containerized with Docker. The deployment utilizes AWS services like ECR (Elastic Container Registry), EC2 (Elastic Compute Cloud), S3 (Simple Storage Service), RDS (Relational Database Service), and ECS Fargate for seamless scaling and deployment.

## Project Workflow

The following steps describe how AWS services are configured and how the CI/CD pipeline is set up to automate the deployment of the dynamic web application.

---

## Steps

### 1. Configure AWS Credentials

To interact with AWS services, I needed to configure your AWS credentials. These will be used by GitHub Actions to interact with AWS services securely.
![Screenshot 2025-03-27 053925](https://github.com/user-attachments/assets/8b9f1b90-4bda-4615-a48b-d9cc6021d85b)

---

### 2. Build AWS Infrastructure with Terraform

Used Terraform to manage and provision the necessary AWS resources, including EC2 instances, S3 buckets, ECR repositories, RDS, and ECS clusters. This will provision the infrastructure resources on AWS.
![Screenshot 2025-03-27 054518](https://github.com/user-attachments/assets/e242646a-91c0-417c-82f0-2b8ad33d0636)

![Screenshot 2025-03-27 053943](https://github.com/user-attachments/assets/3651558e-c089-4485-862f-7ef919669a7b)
![Screenshot 2025-03-27 054005](https://github.com/user-attachments/assets/2ac462fe-4a15-40d4-854b-166c251a0370)
![Screenshot 2025-03-27 054023](https://github.com/user-attachments/assets/bb450ef3-dadf-4bbf-9c9b-70773ad5716b)
![Screenshot 2025-03-27 054043](https://github.com/user-attachments/assets/83aae619-72fc-4308-85ef-6575de09dc25)

---

### 3. Create an ECR Repository

An Amazon Elastic Container Registry (ECR) repository is used to store the Docker images for the dynamic web application.
![Screenshot 2025-03-27 054108](https://github.com/user-attachments/assets/18289fc6-4f1f-4b06-bde3-6b875b4181f5)
![Screenshot 2025-03-27 055507](https://github.com/user-attachments/assets/269c8e59-3ba5-44d5-989f-df1835dd6856)

---


### 4. Start a Self-hosted EC2 Runner

For running the CI/CD pipeline with GitHub Actions, I'll need a self-hosted EC2 runner.
![Screenshot 2025-03-27 054127](https://github.com/user-attachments/assets/12a69b1b-9c36-4c4e-8fa2-2c66b5d8e9be)
![Screenshot 2025-03-27 055544](https://github.com/user-attachments/assets/1d0354f9-bdc8-47b5-a8bc-a727e607e4c1)


---

### 5. Build and Push Docker Image to ECR

GitHub Actions will automate the process of building and pushing the Docker image to the ECR repository.
![Screenshot 2025-03-27 054144](https://github.com/user-attachments/assets/92d1a91e-3154-43cc-a86b-74a2481ffbbe)
![Screenshot 2025-03-27 054202](https://github.com/user-attachments/assets/91c6a474-d1f4-4e23-85eb-999369df4658)
![Screenshot 2025-03-27 055615](https://github.com/user-attachments/assets/95e483a3-dd09-41da-8380-3c9e67bf1f29)


---

### 6. Create an Environment File and Export to S3

An environment file containing necessary configurations (database URL, credentials) is created and uploaded to an S3 bucket.
![Screenshot 2025-03-27 054223](https://github.com/user-attachments/assets/072fa606-8ae4-48ca-bfc4-eb42e1a3fa7b)
![Screenshot 2025-03-27 055649](https://github.com/user-attachments/assets/24b21378-cda0-4e54-8193-820a53c97294)


---

### 7. Migrate Data into the RDS Database with Flyway

Flyway will handle database migrations to ensure the RDS database schema is up to date.
![Screenshot 2025-03-27 054239](https://github.com/user-attachments/assets/cf2a354f-84a9-4bb8-afe9-272c6ffbaacc)
![Screenshot 2025-03-27 055740](https://github.com/user-attachments/assets/9cc6a052-ed81-43f0-ab90-f62bfeb29ec6)


---

### 8. Stop the Self-hosted EC2 Runner

Once the CI/CD pipeline completes, I stopped the self-hosted EC2 runner to save resources.
![Screenshot 2025-03-27 054308](https://github.com/user-attachments/assets/85b19e33-beb9-4a22-9285-25c55fe3545f)


---

### 9. Create a New Task Definition Revision

After the Docker image is pushed to ECR, I created a new task definition revision in ECS.
![Screenshot 2025-03-27 054329](https://github.com/user-attachments/assets/18b4acba-d478-4a87-bf2e-4844e98ab10f)
![Screenshot 2025-03-27 054347](https://github.com/user-attachments/assets/c4008d87-5117-43fd-a0fe-0482d91e1c38)
![Screenshot 2025-03-27 055823](https://github.com/user-attachments/assets/f1d4059b-6202-465f-9d30-631a3f783a26)
![Screenshot 2025-03-27 055859](https://github.com/user-attachments/assets/488fe787-928c-40cb-9845-4627b94c47a5)


---

### 10. Restart the EC2 Fargate Service

Forced a new deployment by restarting the ECS Fargate service using the updated task definition.
![Screenshot 2025-03-27 054402](https://github.com/user-attachments/assets/6a68b588-7b2a-45e4-a1e4-ff4a698c519a)
![Screenshot 2025-03-27 055841](https://github.com/user-attachments/assets/4355fb01-ecdb-420e-ab28-8a55ed788e4c)

---

### Dynamic Web Application Deployment
![Screenshot 2025-03-27 060643](https://github.com/user-attachments/assets/2871818a-9f71-4aeb-aabb-51ac3f07d1ce)

![Screenshot 2025-03-25 234412](https://github.com/user-attachments/assets/1b7aaedf-68e8-41ab-bb1d-85823082bebb)
![Screenshot 2025-03-25 234448](https://github.com/user-attachments/assets/ec16d49f-0f6f-4b72-85d7-ec52c2a6f05e)
![Screenshot 2025-03-25 234510](https://github.com/user-attachments/assets/0989ad78-b0ea-4c21-b06b-76b653d47040)




## Conclusion

In this project, I successfully deployed a dynamic web application on AWS with a fully automated CI/CD pipeline using GitHub Actions. Terraform managed the infrastructure, Docker handled the application containerization, and AWS services such as ECR, EC2, RDS, S3, and ECS Fargate ensured scalability and reliability.


