# Host a Static Website on AWS

## Project Overview
This project involves hosting a static HTML web application on AWS, utilizing a range of AWS services to ensure scalability, reliability, and security. The application is deployed on EC2 instances within a Virtual Private Cloud (VPC) and is accessible via an Application Load Balancer, with automated scaling managed through an Auto Scaling Group.

## Architecture
The project architecture includes the following components:
- **VPC Configuration:** A Virtual Private Cloud (VPC) with both public and private subnets spanning two availability zones.
- **Internet Gateway:** Facilitates connectivity between VPC instances and the Internet.
- **Security Groups:** Act as network firewalls to control inbound and outbound traffic.
- **Availability Zones:** Used to enhance fault tolerance and system reliability.
- **Public Subnets:** For NAT Gateway and Application Load Balancer.
- **EC2 Instance Connect Endpoint:** Ensures secure connections to both public and private subnets.
- **Private Subnets:** Host web servers (EC2 instances) for enhanced security.
- **NAT Gateway:** Allows instances in private subnets to access the Internet.
- **Application Load Balancer:** Distributes traffic across EC2 instances in multiple availability zones.
- **Auto Scaling Group:** Manages EC2 instances for availability, scalability, and fault tolerance.
- **Certificate Manager:** Secures application communications.
- **Simple Notification Service (SNS):** Provides alerts about Auto Scaling Group activities.
- **Route 53:** Manages domain name and DNS records.

## Prerequisites
Before you begin, ensure you have the following:
- An AWS account with permissions to create VPCs, EC2 instances, Load Balancers, Auto Scaling Groups, and other resources.
- A registered domain name (optional but recommended for Route 53).
- Git installed on your local machine.

## Deployment Instructions
1. **Clone the Repository**
```bash
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git
cd host-a-static-website-on-aws
```

2. **Deploy EC2 Instance and Configure Apache**
```bash
#!/bin/bash
sudo su
yum update -y
yum install -y httpd
cd /var/www/html
yum install git -y
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git
cp -R host-a-static-website-on-aws/. /var/www/html/
rm -rf host-a-static-website-on-aws
systemctl enable httpd
systemctl start httpd
```

3. **Set Up VPC and Networking**
- Create a VPC with public and private subnets across two availability zones.
- Configure an Internet Gateway and attach it to the VPC.
- Set up Security Groups for the EC2 instances and Load Balancer.

4. **Configure Load Balancing and Auto Scaling**
- Deploy an Application Load Balancer in the public subnets.
- Configure a target group linked to the EC2 instances.
- Set up an Auto Scaling Group to manage instance scaling.

5. **Enable HTTPS with Certificate Manager**
- Request a public SSL/TLS certificate via AWS Certificate Manager.
- Associate the certificate with the Application Load Balancer.

6. **Set Up Monitoring and Notifications**
- Configure SNS to receive alerts about Auto Scaling Group activities.

7. **Register Domain and Configure DNS with Route 53**
- Create a hosted zone in Route 53 and set up DNS records for the domain.

## Project Diagram
A reference architecture diagram is available in the GitHub repository to provide a visual overview of the infrastructure setup.

## Troubleshooting
- **Web Server Issues:** Ensure Apache is running using `sudo systemctl status httpd`.
- **EC2 Connectivity:** Verify Security Group rules allow HTTP (port 80) and HTTPS (port 443) traffic.
- **Load Balancer Health Checks:** Ensure the health check path is correctly configured to the web server's response page.


## Acknowledgments
Special thanks to all the contributors and open-source tools that made this project possible.


