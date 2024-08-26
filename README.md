
```markdown
# Capstone Project: Introduction to Cloud Computing
## E-Commerce Platform Deployment with Git, Linux, and AWS

**Name:** Ugwu Emeka Ben-Kingsley  
**Position:** Trainee Jnr DevOps Engr

![my_picture](images/benking_pic)

## Project Overview/Scope

This document outlines the process used to develop an e-commerce website for a new online marketplace named “marketPeak.” It includes steps from setting up the environment to deploying the website and troubleshooting issues. The platform features product listings, a shopping cart, and user authentication.

## Objectives

The aim of the project is to:
- Set up a version control system using Git.
- Develop the website in a Linux environment.
- Deploy it on an AWS EC2 instance.

The static website for MarketPeak_Ecommerce includes:
- A home page
- An about us page
- A contact page

## 1.1 Setup: Git Version Control Setup

I already had Git, MobaXterm, and Visual Studio Code installed on my local machine. Here are the steps I followed to set up the project:

1. **Download and Install Git**: Downloaded Git from Google and run the installer from git-scm.com.
2. **Create New Directory**: 
   ```bash
   mkdir Marketpeak_Ecommerce
   ```
3. **Initialize Git**: 
   ```bash
   git init
   ```
4. **Commands Used**:
   ```bash
   mkdir MarketPeak_Ecommerce
   cd MarketPeak_Ecommerce
   git init
   ```

## 1.2 Prepare the E-Commerce Website Template

I prepared the e-commerce website template using a pre-existing template. Downloaded a free template from Tooplate and extracted it into my project folder `MarketPeak_Ecommerce`.

## 1.3 Stage and Commit the Template

Staged and committed the template to Git using the following commands:
```bash
git add .
git config --global user.name "benking-web"
git config --global user.email "ugemeka@yahoo.com"
git commit -m "Initial commit with basic e-commerce site structure"
```

## 1.4 Push the Code to GitHub

1. **Create Remote Repository**: Created a remote repository on GitHub named "MarketPeak_Ecommerce" without initializing it with a README, `.gitignore`, or license.
   [GitHub Repository](https://github.com/benking-web/-MarketPeak_Ecommerce-website.git)
2. **Link Local Repository to GitHub**:
   ```bash
   git remote add origin https://github.com/benking-web/MarketPeak_Ecommerce.git
   ```
3. **Upload Local Repository**:
   ```bash
   git push -u origin main
   ```

## 2.0 AWS Deployment

### 2.1 Set Up an AWS EC2 Instance
When you launch an EC2 instance on Amazon Web Services (AWS), you need to choose an Amazon Machine Image (AMI) that serves as the template for your instance. For Linux-based environments, AWS provides a variety of AMIs to suit different needs. Here's a guide to help you select and work with Linux AMIs on EC2:

### 1. **Choosing a Linux AMI**

AWS offers several Linux AMIs, including:

#### **Amazon Linux AMI**

- **Amazon Linux 2**: The latest version, optimized for AWS and supported by AWS.
  - **Features**: Long-term support, integrated with AWS services, security updates.
  - **Usage**: Great for general-purpose workloads and well-supported by AWS.
  - **Find It**: Search for "Amazon Linux 2" in the AWS Management Console


### 2. **Launching an EC2 Instance with a Linux AMI**

1. **Log in to the AWS Management Console**.

2. **Navigate to the EC2 Dashboard**:
   - Go to "Services" and select "EC2".

3. **Launch Instance**:
   - Click "Launch Instance" to start the instance creation wizard.

4. **Select an AMI**:
   - Choose  AMI  from the list. You can use the search bar to find specific Linux distributions.

5. **Choose an Instance Type**:
   - Select the instance type based on your workload requirements (e.g., t2.micro for light workloads or m5.large for more intensive tasks).

6. **Configure Instance Details**:
   - Set up network settings, IAM roles, and other configurations.

7. **Review and Launch**:
    - Review your settings and click "Launch". You will be prompted to select or create a key pair for SSH access.

8. **Connect to Your Instance**:
    - After launching, go to the "Instances" page, select your instance, and click "Connect" to get instructions for connecting via SSH.

### 3. **Configuring Your Linux Instance**

Once your instance is up and running, you might want to configure it further:

- **Update Packages**: 
  ```bash
  sudo apt-get update  
  sudo yum update                               
  ```

- **Install Necessary Software**:
  ```bash
  sudo apt-get install <Ubuntu/Debian> 
  sudo yum install <Amazon Linux>      
  ```


1. Logged into AWS Management Console and launched an EC2 instance using an Amazon Linux AMI.
2. Connected to the instance using SSH.

### 2.2 Clone Repository on Linux Server

1. Navigated to my repository in GitHub.
2. Selected the code: [GitHub Repository](https://github.com/benking-web/-MarketPeak_Ecommerce-website.git)
3. On my EC2 instance, generated an SSH key pair using Keygen and copied the public key:
   ```bash
   cat /home/ec2-user/.ssh/id_rsa.pub
   ```
4. Added the SSH public key to my GitHub account.
5. Cloned the repository using the SSH clone URL:
   ```bash
   git clone git@github.com:benking-web/MarketPeak_Ecommerce.git
   ```

### 2.3 Install a Web Server on EC2

1. Installed Apache HTTP Server (`httpd`) on the EC2 server to host MarketPeak E-commerce site:
   ```bash
   sudo yum update -y
   sudo yum install httpd -y
   sudo systemctl start httpd
   sudo systemctl enable httpd
   ```

### 2.4 Configure `httpd` for Website

1. Clear the default `httpd` web directory and copy MarketPeak E-commerce website files to it:
   ```bash
   sudo rm -rf /var/www/html/*
   sudo cp -r ~/MarketPeak_Ecommerce/* /var/www/html/
   ```
   *Note:* When you install Apache on a Linux system, it automatically creates this directory as the default document root.

2. Reload `httpd`:
   ```bash
   sudo systemctl reload httpd
   ```

### 2.5 Access Website from Browser

With `httpd` configured and website files in place, MarketPeak E-commerce platform is now live. Open a web browser and access the public IP of your EC2 instance to view the deployed website.

## 3.0 Continuous Integration and Deployment Workflow

### Step 1: Develop New Features and Fixes

1. Create a new branch for development:
   ```bash
   git branch development
   git checkout development
   ```
2. Implement changes (e.g., update web pages, add new products, or fix issues).

### Step 2: Version Control with Git

1. Stage and add changes:
   ```bash
   git add .
   ```
2. Commit changes:
   ```bash
   git commit -m "Add new features or fix bugs"
   ```
3. Push changes to GitHub:
   ```bash
   git push origin development
   ```

### Step 3: Pull Requests and Merging

1. Switch to the main branch and merge:
   ```bash
   git checkout main
   git merge development
   ```
2. Push merged changes to GitHub:
   ```bash
   git push origin main
   ```

### Step 4: Deploying Updates to the Production Server

1. SSH into the AWS EC2 instance where the production website is hosted.
2. Navigate to the website directory and pull the latest changes:
   ```bash
   git pull origin main
   ```
3. Restart the web server:
   ```bash
   sudo systemctl reload httpd
   ```

### Step 5: Testing the New Changes

1. Access the website by opening a web browser and navigating to the public IP address of your EC2 instance.
2. Test new features or fixes to ensure they work as expected.

## Challenges Faced and Solutions

### 1. Configuration Management

**Challenge:** Ensuring configuration settings are correct across different environments.

**Solution:**
-using the correct pem key
- using window with a larger memory X86 
### 2. Version Control with Git

**Challenge:** Managing code changes and deployments through Git.

**Solution:**
- Adopt a branching strategy like Git Flow or GitHub Flow.
- using the correct key pair.

### 3. Server Setup and Maintenance

**Challenge:** Setting up and maintaining servers on Linux.

**Solution:**
- Leverage AWS Elastic Beanstalk or AWS Lightsail for easier deployment.
- Follow best practices for Linux server security.

### 4. Database Management

**Challenge:** Configuring and managing the database.

**Solution:**
- use AWS free tier help to stayed connected without payment.

- # My Images

## Image 1

![clone image](![ec2 gitclone](https://github.com/user-attachments/assets/5866fd56-f7e3-40ed-9d5d-7bd2123a6dc5)


## Image 2
![git init 2](![Screenshot 2024-08-10 042102](https://github.com/user-attachments/assets/558e77ec-58a3-48c3-a42b-6febc69dd5da)


## Image 3
![git config 3](![Screenshot 2024-08-10 042220](https://github.com/user-attachments/assets/1e97836c-9664-4192-86a0-299bab9e39f9)

## image 4
![image 4](![![Screenshot 2024-08-10 042448](https://github.com/user-attachments/assets/0405cc7c-007c-4705-bc96-e5eac795de11)
## image 5
![image 5](![![Screenshot 2024-08-10 042448](https://github.com/user-attachments/assets/0405cc7c-007c-4705-bc96-e5eac795de11)

## image 6

![image 6](![Screenshot 2024-08-10 042806](https://github.com/user-attachments/assets/81bfebf8-059d-497b-ae7e-ebb028f8ab9b)



## image 7

![image 7](![![Screenshot 2024-08-10 043042](https://github.com/user-attachments/assets/48473156-f5a8-479f-b5a1-91b2d16a06ab)

## image 8

![image 7](![Screenshot 2024-08-10 042656](https://github.com/user-attachments/assets/7fc859a4-cf73-4044-8f3b-77f63cbc1588)

## image 9

![image 7](![Screenshot 2024-08-10 042656](https://github.com/user-attachments/assets/7fc859a4-cf73-4044-8f3b-77f63cbc1588)


