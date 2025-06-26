![image](https://github.com/user-attachments/assets/fd920870-a66b-45a3-8c38-954855eff6d4)
Project 1: Scalable Web Application with ALB and Auto Scaling
Architecture: EC2-based
Description:
Deploy a simple web application on AWS using EC2 instances, ensuring high availability and scalability with Elastic Load Balancing (ALB) and Auto Scaling Groups (ASG). The project demonstrates best practices for compute scalability, security, and cost optimization.
Key AWS Services Used:
EC2: Launch instances for the web app.
Application Load Balancer (ALB): Distributes traffic across multiple instances.
Auto Scaling Group (ASG): Ensures instances scale based on demand.
Amazon RDS (Optional): Backend database (MySQL/PostgreSQL) with Multi-AZ.
IAM: Role-based access to instances.
CloudWatch & SNS: Monitor performance and send alerts.

Project Description:

In this project, I built a robust 3-tier architecture on AWS .

The architecture consists of:

1. Web Application Tier (Presentation Layer): This tier handles the user interface and user experience, providing a seamless interaction platform for customers. Thinking of an online clothing store, this is where customers browse through clothing items, view details of each product, add items to their cart, and proceed to checkout.

2. Application Tier (Business Logic): This tier processes the core functionalities of the e-commerce platform, including order processing, user authentication, and product catalog management. In the context of an online clothing store, this tier manages the logic for adding items to the cart, processing payments, managing user accounts, and updating inventory levels.

3. Data Tier (Database): This tier securely stores all the critical data, such as customer information, transaction records, and product details. For an online clothing store, this includes storing details of each clothing item, customer profiles, order histories, and payment information.

Key Components and Services:

1. VPC and Subnets: Network infrastructure that segregates and secures different layers of the application.

2. NAT Gateways and Route Tables: Manage internet traffic efficiently, ensuring secure and reliable connectivity for private instances.

3. Auto Scaling Groups and Load Balancers: Ensure high availability and scalability, automatically adjusting to traffic demands and balancing loads across instances.

4. AWS Systems Manager (SSM): Facilitates secure and seamless connection to our instances without needing a bastion host or opening ports, thus enhancing security by reducing potential attack surfaces.

5. Amazon S3: Used for storing static assets and backup data, connected securely through a VPC endpoint to ensure data transfers do not traverse the public internet.

6. AWS WAF: Protects our application from common web exploits and vulnerabilities, ensuring a secure environment for our application.

7. Amazon CloudFront: Provides fast content delivery by caching content closer to users, reducing latency and improving the overall user experience.

   IAM Roles
    EC2 Instance Role
Purpose: Allow EC2 instances to interact with AWS services like S3, CloudWatch, and Parameter Store.

Permissions:

AmazonEC2RoleforSSM (for AWS Systems Manager session access)

AmazonS3ReadOnlyAccess ( EC2 needs to fetch from S3)
```
{
  "Effect": "Allow",
  "Action": [
    "s3:GetObject",
    "cloudwatch:PutMetricData",
    "ssm:GetParameter",
    "ec2:DescribeInstances"
  ],
  "Resource": "*"
}
```
SNS (Simple Notification Service):

Purpose: SNS could be integrated for sending notifications on scaling events, health check failures, or security alerts.

Permissions:

sns:Publish for EC2 or Lambda functions to send messages to an SNS topic.

IAM role granting specific services permission to publish/subscribe to topics.
```
{
  "Effect": "Allow",
  "Action": "sns:Publish",
  "Resource": "arn:aws:sns:us-east-1:123456789012:MyTopic"
}
```
