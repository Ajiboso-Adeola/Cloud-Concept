# Task 2
## Goal: Challenge students’ architectural thinking without requiring an AWS account.

**Student Task** <br>
- Write an essay answering this scenario:
>A startup wants to host a basic web application for customers in two countries. The application should be reliable, secure, and easy to grow over time. Propose an AWS-based architecture using appropriate AWS services and explain your decisions.

**Requirements**
- The essay must discuss:<br>
    - Cloud computing benefits
    -  AWS Regions and Availability Zones
    -  EC2 for compute
    -  S3 for storage/static assets/backups
    - IAM users vs roles
    - Security Groups 

## Cloud Computing Benefits
Cloud computing offers several advantages that are critical for startups:
- Cost Efficiency – The startup only pays for resources used instead of investing in physical servers.
- Scalability – Resources can automatically scale up or down based on user demand.
- High Availability – Cloud platforms like AWS distribute infrastructure across multiple data centers.
- Global Reach – Applications can be deployed closer to users in different countries using AWS Regions.
- Security and Compliance – AWS provides built-in security tools such as IAM, encryption, and network isolation.

## AWS Regions and Availability Zones
AWS infrastructure is organized into Regions and Availability Zones (AZs).

A Region is a geographic location (e.g., Europe, US, Africa) that contains multiple isolated data centers.

Each Region contains multiple Availability Zones, which are physically separate data centers designed to protect against failures.
For this startup:
We would deploy the application in two AWS Regions, one closer to each country’s users (e.g., Europe Region and Africa/Europe nearby Region depending on latency).

Within each Region, we would use at least two Availability Zones to ensure fault tolerance.

If one AZ fails, traffic automatically shifts to another AZ, ensuring continuous availability.

## Compute Layer Using Amazon EC2
The core application will run on Amazon EC2 (Elastic Compute Cloud) instances.

- EC2 provides virtual servers where the startup can deploy its web application.

- Instances can be scaled horizontally by adding more servers when traffic increases.

- An Auto Scaling Group can be used to automatically add or remove EC2 instances based on demand.

To improve reliability:
- EC2 instances should be deployed across multiple Availability Zones.
- A load balancer can distribute traffic evenly between instances.

## Storage Using Amazon S3
For storage and static content, the startup will use Amazon S3 (Simple Storage Service).
S3 will be used for:
- Static website assets (images, CSS, JavaScript files)
- Backups and database snapshots
- Application logs and media uploads
S3 is highly durable and stores data across multiple Availability Zones automatically, making it an excellent choice for reliable storage. It also integrates easily with EC2-based applications.

## IAM: Users vs Roles
Security in AWS is managed using IAM (Identity and Access Management).
There are two key concepts:
**IAM Users**
- Represent real people (developers, administrators).
- Each user has credentials (passwords or access keys).
- Best practice: give users only the permissions they need.

**IAM Roles**
- Used by AWS services (like EC2) rather than individuals.
- Allow temporary, secure access without hardcoding credentials.
- Example: an EC2 instance accessing S3 should use an IAM role, not a user account.
- Best practice: Prefer IAM roles over IAM users for applications and services to improve security.

## Security Groups (Network Security)
Security Groups act as virtual firewalls for EC2 instances.
For this architecture:
- Allow inbound traffic only on required ports (e.g., HTTP port 80, HTTPS port 443).
- Restrict SSH access (port 22) to specific IP addresses (e.g., company office IP).
- Deny all unnecessary inbound traffic by default.

Security Groups are stateful, meaning return traffic is automatically allowed, simplifying configuration while maintaining security.

## SSH Key Access Best Practices
To securely access EC2 instances, SSH keys should be used instead of passwords.
Best practices include:
- Generate strong key pairs using modern encryption (e.g., RSA 2048+ or ED25519).
- Never share private keys.
- Store private keys securely (not in public repositories).
- Rotate keys periodically.
- Disable password-based SSH login entirely.
- Use bastion hosts or AWS Systems Manager Session Manager for additional security.

## Architectural Diagram
<img src="./Architectural diagram.svg" width="600" height="600">

