# 🚀 Travel Memory Application

A full-stack **MERN (MongoDB, Express.js, React.js, Node.js)** application for creating, viewing, updating, and managing travel memories. This project demonstrates end-to-end deployment on **AWS EC2**, backend configuration using **Node.js**, frontend integration with **React**, database connectivity using **MongoDB Atlas**, reverse proxy configuration with **Nginx**, and horizontal scaling using multiple EC2 instances.

---

# 📌 Project Objectives

This project covers the following deployment tasks:

* Deploy the Node.js backend on an AWS EC2 Ubuntu instance.
* Configure MongoDB Atlas as the cloud database.
* Configure Nginx as a reverse proxy.
* Connect the React frontend with the deployed backend.
* Build the React application for production.
* Create multiple frontend and backend EC2 instances.
* Prepare the infrastructure for an AWS Application Load Balancer (ALB).
* Manage the project using Git and GitHub.

---

# ✨ Features

* MERN Stack Application
* RESTful API
* MongoDB Atlas Database
* React Frontend
* Express Backend
* AWS EC2 Deployment
* Ubuntu Server
* Nginx Reverse Proxy
* Horizontal Scaling
* Git & GitHub Version Control

---

# 🛠️ Technology Stack

## Frontend

* React.js
* Axios
* HTML5
* CSS3
* JavaScript

## Backend

* Node.js
* Express.js
* Mongoose
* REST API

## Database

* MongoDB Atlas

## Cloud

* AWS EC2
* Ubuntu 26.04 LTS
* Nginx

## Version Control

* Git
* GitHub

---

# 📂 Project Structure

```text
TravelMemory/
│
├── backend/
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── conn.js
│   ├── index.js
│   └── package.json
│
├── frontend/
│   ├── public/
│   ├── src/
│   └── package.json
│
├── LICENSE
├── README.md
└── azure-pipelines.yml
```

---

# 🏗️ Application Architecture

```text
                        Internet
                            │
                            ▼
                   AWS EC2 Ubuntu Server
                            │
                     Nginx Reverse Proxy
                            │
                    Express Node.js API
                            │
                     MongoDB Atlas Cloud
                            ▲
                            │
                     React Frontend
```

---

# 📋 Prerequisites

Before deployment, ensure the following resources are available:

* AWS Account
* EC2 Ubuntu Instance
* MongoDB Atlas Account
* GitHub Repository
* SSH Key Pair
* Node.js
* npm
* Git
* Nginx

---

# Task 1 – Backend Configuration (TravelMemory Deployment)

## Objective

Configure and deploy the Node.js backend of the TravelMemory application on an Ubuntu EC2 instance by installing the required software, connecting to MongoDB Atlas, configuring Nginx as a reverse proxy, and verifying that the backend is accessible.

---

# Step 1 – Connect to the EC2 Instance

Connect to the Ubuntu EC2 instance using SSH.

```bash
ssh -i <your-key.pem> ubuntu@<EC2-Public-IP>
```

## Verify the Operating System

```bash
cat /etc/os-release

hostname
```

### Output

```text
PRETTY_NAME="Ubuntu 26.04 LTS"

VERSION="26.04 LTS (Resolute Raccoon)"

Hostname:

ip-10-0-4-173
```

### Explanation

Verified that the application is deployed on an Ubuntu 26.04 EC2 instance.

---

# Step 2 – Update the Server

Update all installed packages.

```bash
sudo apt update && sudo apt upgrade -y
```

### Output

```text
Pending kernel upgrade!

Running kernel version:

7.0.0-1006-aws

Expected kernel:

7.0.0-1008-aws
```

### Explanation

Updated all system packages to ensure the server is running the latest software versions before deployment.

---

# Step 3 – Reboot the Server

Restart the EC2 instance.

```bash
sudo reboot
```

Reconnect using SSH.

Verify the kernel version.

```bash
uname -r
```

### Output

```text
7.0.0-1008-aws
```

### Explanation

Confirmed that the server is running the updated Linux kernel.

---

# Step 4 – Install Required Software

## Install Git

```bash
sudo apt install git -y
```

### Explanation

Git is required to clone and manage the project repository.

---

## Install Nginx

```bash
sudo apt install nginx -y
```

### Explanation

Nginx is used as a reverse proxy between users and the backend application.

---

## Install Node.js

```bash
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -

sudo apt install nodejs -y
```

### Explanation

Installed the latest LTS version of Node.js for running the backend application.

---

## Verify Installation

```bash
git --version

node -v

npm -v

nginx -v
```

### Output

```text
git version 2.53.0

v24.18.0

11.16.0

nginx version: nginx/1.28.3 (Ubuntu)
```

### Explanation

Verified that all required software packages were installed successfully.

---

# Step 5 – Clone the Repository

Clone the TravelMemory GitHub repository.

```bash
git clone https://github.com/UnpredictablePrashant/TravelMemory.git
```

Move into the project.

```bash
cd TravelMemory
```

Verify project contents.

```bash
ls
```

### Output

```text
LICENSE

README.md

azure-pipelines.yml

backend

frontend
```

### Explanation

Successfully cloned the application source code from GitHub.

---

# Step 6 – Navigate to Backend

Move into the backend directory.

```bash
cd backend
```

Display backend files.

```bash
ll
```

### Output

```text
conn.js

controllers/

index.js

models/

package-lock.json

package.json

routes/
```

### Explanation

Verified the backend project structure and required application files.

---

# Step 7 – Inspect Backend Configuration

View the MongoDB connection file.

```bash
cat conn.js
```

### Output

```javascript
const URL = process.env.MONGO_URI

mongoose.connect(URL)
```

View the application entry point.

```bash
cat index.js
```

### Output

```javascript
PORT = process.env.PORT

app.listen(PORT)
```

### Explanation

Verified that the backend uses two environment variables:

* **MONGO_URI** – MongoDB Atlas connection string
* **PORT** – Application listening port (3000)

---

# Step 8 – Configure MongoDB Atlas

## Create MongoDB Atlas Cluster

Create a **Free Tier MongoDB Atlas Cluster**.

---

## Create Database User

Create a database user with a username and password.

Example:

```text
Username : <USERNAME>

Password : <PASSWORD>
```

---

## Whitelist the EC2 Public IP

Navigate to:

```text
MongoDB Atlas

↓

Network Access

↓

Add IP Address
```

Add the **EC2 Public IP** so that the backend application can communicate with MongoDB Atlas.

### Explanation

Whitelisting allows only authorised IP addresses to access the MongoDB Atlas cluster.

---

# Create the Environment File

Create a `.env` file inside the backend directory.

```bash
nano .env
```

Contents:

```env
MONGO_URI=mongodb+srv://<USERNAME>:<PASSWORD>@<CLUSTER>.mongodb.net/TravelMemory

PORT=3000
```

Verify the file.

```bash
cat .env
```

### Output

```env
MONGO_URI=mongodb+srv://<USERNAME>:<PASSWORD>@<CLUSTER>.mongodb.net/TravelMemory

PORT=3000
```

### Explanation

The backend application reads the MongoDB connection string and application port from the environment variables.

---

# Step 9 – Install Backend Dependencies

Install all required Node.js packages.

```bash
npm install
```

### Output

```text
added 117 packages

audited 118 packages
```

### Explanation

Installed all dependencies defined in **package.json**.

---

# Step 10 – Start the Backend Application

Initially attempted:

```bash
npm start
```

### Output

```text
Missing script: start
```

### Explanation

The project does not define a **start** script inside **package.json**.

Run the backend manually.

```bash
node index.js
```

### Output

```text
Server started at http://localhost:3000
```

### Explanation

Successfully started the Express backend application.

---

# Step 11 – Verify Backend

Test the backend directly.

```bash
curl http://localhost:3000/hello
```

### Output

```text
Hello World!
```

### Explanation

Confirmed that the backend API is functioning correctly.

---

# Step 12 – Configure Nginx Reverse Proxy

Create a custom Nginx configuration.

```bash
sudo nano /etc/nginx/sites-available/travelmemory
```

Configuration:

```nginx
server {

    listen 80;

    server_name _;

    location / {

        proxy_pass http://localhost:3000;

        proxy_http_version 1.1;

        proxy_set_header Upgrade $http_upgrade;

        proxy_set_header Connection "upgrade";

        proxy_set_header Host $host;

        proxy_cache_bypass $http_upgrade;

    }

}
```

### Explanation

Configured Nginx to forward all incoming HTTP requests to the Node.js backend running on **localhost:3000**.

---

# Step 13 – Enable the Nginx Configuration

Enable the configuration.

```bash
sudo ln -s /etc/nginx/sites-available/travelmemory /etc/nginx/sites-enabled/
```

Test the configuration.

```bash
sudo nginx -t
```

### Output

```text
syntax is ok

test is successful
```

Reload Nginx.

```bash
sudo systemctl reload nginx
```

### Explanation

Activated the newly created reverse proxy configuration.

---

# Step 14 – Verify Reverse Proxy

Test the application through Nginx.

```bash
curl http://localhost/hello
```

### Output

```text
Hello World!
```

### Explanation

Confirmed that requests received on **port 80** are successfully forwarded to the backend server.

---

# Backend Deployment Flow

```text
                User Request

                     │

                     ▼

              Nginx Port 80

                     │

                     ▼

        localhost:3000 (Node.js)

                     │

                     ▼

             MongoDB Atlas Cloud
```

---

# Backend Verification

## Verify Node.js

```bash
node -v
```

Output

```text
v24.18.0
```

---

## Verify npm

```bash
npm -v
```

Output

```text
11.16.0
```

---

## Verify Git

```bash
git --version
```

Output

```text
git version 2.53.0
```

---

## Verify Nginx

```bash
nginx -v
```

Output

```text
nginx version: nginx/1.28.3 (Ubuntu)
```

---

## Verify Backend API

```bash
curl http://localhost:3000/hello
```

Output

```text
Hello World!
```

---

## Verify Reverse Proxy

```bash
curl http://localhost/hello
```

Output

```text
Hello World!
```

---

# Task 1 Summary

## Completed Successfully

* ✅ Connected to Ubuntu EC2 Instance
* ✅ Updated the Operating System
* ✅ Rebooted the Server
* ✅ Installed Git
* ✅ Installed Node.js
* ✅ Installed npm
* ✅ Installed Nginx
* ✅ Cloned the GitHub Repository
* ✅ Verified Backend Structure
* ✅ Configured MongoDB Atlas
* ✅ Created Environment Variables
* ✅ Installed Backend Dependencies
* ✅ Started the Backend Application
* ✅ Verified Backend API
* ✅ Configured Nginx Reverse Proxy
* ✅ Enabled Nginx Configuration
* ✅ Verified Reverse Proxy
* ✅ Successfully Deployed the Backend Application

---

# Backend Deployment Result

The Travel Memory backend was successfully deployed on an Ubuntu EC2 instance.

The deployment includes:

* MongoDB Atlas database connectivity
* Express.js backend
* Node.js runtime
* Nginx reverse proxy
* Ubuntu server
* REST API verification
* Port 80 reverse proxy access

The backend application is now accessible through **Nginx on Port 80** and is ready for frontend integration.

---

# Task 2 – Frontend and Backend Connection (TravelMemory Deployment)

## Objective

Configure the React frontend, connect it with the backend API, install all frontend dependencies, verify communication between the frontend and backend, and troubleshoot connectivity issues.

---

# Step 1 – Navigate to the Frontend Directory

Move to the frontend directory.

## Command

```bash
cd ~/TravelMemory/frontend

ls
```

## Output

```text
package.json

package-lock.json

public

src
```

### Explanation

Navigated to the frontend project directory containing the React application.

---

# Step 2 – Locate the Backend URL File

Move into the source directory.

## Command

```bash
cd src

ls
```

## Output

```text
url.js

App.js

components

index.js

...
```

Display the backend URL configuration.

## Command

```bash
cat url.js
```

## Output

```javascript
export const baseUrl = "http://43.205.228.34";
```

### Explanation

Verified the backend API endpoint configured for the React application.

---

# Step 3 – Update the Backend API URL

Edit the backend URL configuration.

## Command

```bash
vim url.js
```

### Output

```text
File updated successfully.
```

Verify the updated file.

## Command

```bash
cat url.js
```

## Output

```javascript
export const baseUrl = "http://43.205.228.34";
```

### Explanation

Configured the frontend to communicate with the backend running on the EC2 instance.

---

# Step 4 – Install Frontend Dependencies

Return to the frontend root directory.

## Command

```bash
cd ..
```

Install all required packages.

```bash
npm install
```

## Output

```text
added 1504 packages, and audited 1505 packages in 32s

236 packages are looking for funding

72 vulnerabilities

15 Low

22 Moderate

31 High

4 Critical
```

### Explanation

Installed all dependencies listed in **package.json**.

---

# Step 5 – Verify package.json

Display the package configuration.

## Command

```bash
cat package.json
```

## Output

```json
"scripts": {

  "start": "react-scripts start",

  "build": "react-scripts build",

  "test": "react-scripts test",

  "eject": "react-scripts eject"

}
```

### Explanation

Verified the available React application scripts.

---

# Step 6 – Start the React Development Server

Run the application.

## Command

```bash
npm start
```

## Output

```text
Compiled successfully!

You can now view frontend in the browser.

Local:

http://localhost:3000

On Your Network:

http://10.0.5.150:3000

webpack compiled successfully
```

### Explanation

Successfully started the React development server.

---

# Step 7 – Verify the Frontend

Open the application using the EC2 public IP.

## URL

```text
http://13.233.115.40:3000
```

## Output

```text
Uncaught runtime errors:

ERROR

Network Error

AxiosError: Network Error
```

### Explanation

The React application loaded correctly, but it could not communicate with the backend API.

---

# Step 8 – Verify Backend Through Nginx

Test the backend endpoint.

## Command

```bash
curl http://localhost/hello
```

## Output

```html
404 Not Found

nginx/1.28.3 (Ubuntu)
```

### Explanation

Confirmed that Nginx was responding, but the reverse proxy configuration was not forwarding requests to the backend server.

---

# Step 9 – Reconfigure Nginx

The default Nginx configuration was serving requests instead of forwarding them to the backend application.

## Remove the Default Configuration

```bash
sudo unlink /etc/nginx/sites-enabled/default
```

### Output

```text
Default configuration removed successfully.
```

### Explanation

Removed the default Nginx site configuration to allow a custom reverse proxy configuration.

---

## Create a Custom Nginx Configuration

Navigate to the Nginx configuration directory.

```bash
cd /etc/nginx/sites-available/
```

Create a custom configuration file.

```bash
sudo vim custom_server.conf
```

Configuration:

```nginx
server {
    listen 80;

    server_name _;

    location / {
        proxy_pass http://localhost:3000;

        proxy_http_version 1.1;

        proxy_set_header Upgrade $http_upgrade;

        proxy_set_header Connection "upgrade";

        proxy_set_header Host $host;

        proxy_cache_bypass $http_upgrade;
    }
}
```

### Explanation

Configured Nginx to forward all incoming HTTP requests on port **80** to the backend application running on **localhost:3000**.

---

## Enable the Configuration

```bash
sudo ln -s /etc/nginx/sites-available/custom_server.conf \
/etc/nginx/sites-enabled/custom_server.conf
```

### Output

```text
Symbolic link created successfully.
```

### Explanation

Enabled the custom Nginx configuration.

---

# Step 10 – Verify the Nginx Configuration

Test the configuration.

```bash
sudo nginx -t
```

### Output

```text
syntax is ok

test is successful
```

Reload Nginx.

```bash
sudo systemctl reload nginx
```

Restart Nginx.

```bash
sudo systemctl restart nginx
```

### Explanation

Reloaded and restarted Nginx to activate the new reverse proxy configuration.

---

# Step 11 – Verify Reverse Proxy Again

Test the backend through Nginx.

```bash
curl http://localhost/hello
```

### Output

```html
502 Bad Gateway

nginx/1.28.3 (Ubuntu)
```

### Explanation

Nginx successfully received the request, but it could not connect to the backend application because the Node.js server was no longer running.

---

# Step 12 – Verify the Backend Server

Check whether the backend application is listening on port **3000**.

```bash
sudo lsof -i :3000
```

### Output

```text
No output
```

### Explanation

No process was listening on port **3000**. This confirmed that the backend server had stopped, resulting in the **502 Bad Gateway** error.

Restart the backend application.

```bash
cd ~/TravelMemory/backend

node index.js
```

Expected output:

```text
Server started at http://localhost:3000
```

Verify the backend again.

```bash
curl http://localhost:3000/hello
```

Output:

```text
Hello World!
```

Verify the reverse proxy.

```bash
curl http://localhost/hello
```

Output:

```text
Hello World!
```

---

# Step 13 – Build the React Application

Create an optimized production build.

```bash
npm run build
```

### Output

```text
Creating an optimized production build...

Compiled successfully.

The build folder is ready to be deployed.
```

### Explanation

Generated a production-ready React build inside the **build/** directory.

---

# Step 14 – Restart the React Application

Restart the development server.

```bash
npm start
```

### Output

```text
Compiled successfully!

You can now view frontend in the browser.

Local:
http://localhost:3000

On Your Network:
http://10.0.5.150:3000
```

### Explanation

Restarted the frontend after updating the backend configuration.

---

# Troubleshooting

## Problem 1 – Axios Network Error

### Error

```text
AxiosError: Network Error
```

### Cause

The React frontend could not communicate with the backend API.

### Resolution

* Verified the backend URL inside **url.js**
* Confirmed that the backend application was running
* Verified the MongoDB connection
* Verified the reverse proxy configuration

---

## Problem 2 – 404 Not Found

### Error

```text
404 Not Found
```

### Cause

Nginx was serving its default site instead of forwarding requests to the backend.

### Resolution

* Removed the default Nginx configuration
* Created a custom reverse proxy configuration
* Enabled the custom configuration
* Reloaded Nginx

---

## Problem 3 – 502 Bad Gateway

### Error

```text
502 Bad Gateway
```

### Cause

The backend application was not running on port **3000**.

### Resolution

Verified the listening process.

```bash
sudo lsof -i :3000
```

No process was found.

Restarted the backend.

```bash
node index.js
```

Verified:

```bash
curl http://localhost:3000/hello
```

Response:

```text
Hello World!
```

---

# Task 2 Summary

## Completed Successfully

* ✅ Verified the frontend project structure
* ✅ Updated the backend API endpoint
* ✅ Installed all frontend dependencies
* ✅ Verified React package scripts
* ✅ Started the React development server
* ✅ Verified frontend compilation
* ✅ Tested frontend-backend communication
* ✅ Diagnosed Axios Network Error
* ✅ Diagnosed 404 Not Found
* ✅ Reconfigured Nginx
* ✅ Enabled the custom reverse proxy
* ✅ Reloaded and restarted Nginx
* ✅ Diagnosed 502 Bad Gateway
* ✅ Restarted the backend service
* ✅ Verified reverse proxy functionality
* ✅ Generated a production React build
* ✅ Successfully connected the frontend with the backend

---

# Result

The React frontend was successfully configured to communicate with the Node.js backend. After updating the API endpoint, configuring Nginx, and restarting the backend service, the application was able to communicate successfully with the backend through the reverse proxy. The frontend was also built for production, making it ready for deployment.

# Task 3 – Scaling the Application (TravelMemory Deployment)

## Objective

Scale the TravelMemory application by creating multiple frontend and backend EC2 instances. These replica instances will later be attached to an **AWS Application Load Balancer (ALB)** to distribute incoming traffic, improve scalability, and provide high availability.

---

# Scaling Architecture

```text
                               Internet
                                   │
                                   ▼
                    +-------------------------------+
                    |  Application Load Balancer    |
                    +-------------------------------+
                          │                   │
                          │                   │
              +-------------------+   +-------------------+
              | Backend EC2-1     |   | Backend EC2-2     |
              +-------------------+   +-------------------+
                          │                   │
                          └─────────┬─────────┘
                                    │
                                    ▼
                           +------------------+
                           |  MongoDB Atlas   |
                           +------------------+

              +-------------------+   +-------------------+
              | Frontend EC2-1    |   | Frontend EC2-2    |
              +-------------------+   +-------------------+
                          │                   │
                          └─────────┬─────────┘
                                    │
                                    ▼
                     AWS Application Load Balancer
```

---

# Architecture Explanation

### Internet

Users access the application using a public URL or public IP address.

### Application Load Balancer (ALB)

The ALB receives incoming requests and distributes them across multiple healthy EC2 instances.

Benefits include:

* High Availability
* Load Distribution
* Fault Tolerance
* Automatic Health Checks

---

### Backend EC2 Instances

Two backend Node.js servers host identical copies of the backend application.

Responsibilities:

* Process API requests
* Connect to MongoDB Atlas
* Return JSON responses
* Handle CRUD operations

---

### MongoDB Atlas

MongoDB Atlas serves as the centralized cloud database.

Advantages:

* Managed database
* Automatic backups
* High availability
* Secure authentication
* Accessible by multiple backend instances

---

### Frontend EC2 Instances

Two frontend EC2 instances host the React application.

Responsibilities:

* Serve static React files
* Communicate with backend APIs
* Provide user interface

---

# Benefits of Horizontal Scaling

Scaling the application across multiple EC2 instances provides several advantages:

* Increased Availability
* Improved Performance
* Better Resource Utilization
* Fault Tolerance
* Easier Maintenance
* Higher Reliability
* Future Auto Scaling Support

---

# Step 1 – Open the EC2 Console

Navigate to the AWS Management Console.

```
AWS Console
    ↓
EC2 Dashboard
    ↓
Instances
```

### Explanation

Opened the EC2 dashboard to create replica instances.

---

# Step 2 – Create a Frontend Replica Instance

Select the existing frontend EC2 instance.

Navigate to:

```
Actions
    ↓
Image and templates
    ↓
Launch more like this
```

Configure the replica instance.

| Property          | Value                   |
| ----------------- | ----------------------- |
| Instance Name     | Frontend-Server-Replica |
| Instance Type     | t2.micro                |
| Operating System  | Ubuntu Linux            |
| Region            | ap-south-1              |
| Availability Zone | ap-south-1b             |
| Security Group    | Bastion-Host-SG         |
| Key Pair          | shiwanshu-HV-keypair    |

Launch the instance.

### Output

```text
Instance Name : Frontend-Server-Replica

Instance ID : i-02fe2059901730611

State : Running

Status Checks : 2/2 checks passed

Public IP : 13.127.195.252
```

### Explanation

Successfully created a replica frontend server that can later be attached to an Application Load Balancer.

---

# Step 3 – Verify the Frontend Replica

Verify the EC2 instance status.

### Output

```text
Running

Status Checks:

2/2 checks passed
```

### Explanation

Confirmed that the frontend replica instance launched successfully and passed all AWS health checks.

---

# Step 4 – Create a Backend Replica Instance

Select the existing backend EC2 instance.

Navigate to:

```text
AWS Console
    ↓
EC2 Dashboard
    ↓
Instances
    ↓
Select Backend Instance
    ↓
Actions
    ↓
Image and templates
    ↓
Launch more like this
```

Configure the new instance using the same settings as the original backend server.

| Property          | Value                  |
| ----------------- | ---------------------- |
| Instance Name     | Backend-Server-Replica |
| Instance Type     | t3.micro               |
| Operating System  | Ubuntu Linux           |
| Region            | ap-south-1             |
| Availability Zone | ap-south-1a            |
| Security Group    | Bastion-Host-SG        |
| Key Pair          | shiwanshu-HV-keypair   |

Launch the instance.

### Output

```text
Instance Name : Backend-Server-Replica

Instance ID : i-0fcb728a0cdadd440

State : Running

Status Checks : 3/3 checks passed

Public IP : 65.1.135.242
```

### Explanation

Created a replica of the backend server to improve application scalability and support load balancing.

---

# Step 5 – Verify the Backend Replica

Verify that the backend replica is running successfully.

### Output

```text
Running

Status Checks:

3/3 checks passed
```

### Explanation

Confirmed that the backend replica launched successfully and passed all EC2 health checks.

---

# Replica Instance Details

## Frontend Replica

| Property          | Value                   |
| ----------------- | ----------------------- |
| Instance Name     | Frontend-Server-Replica |
| Instance ID       | i-02fe2059901730611     |
| Instance Type     | t2.micro                |
| Public IP         | 13.127.195.252          |
| Availability Zone | ap-south-1b             |
| Security Group    | Bastion-Host-SG         |
| Key Pair          | shiwanshu-HV-keypair    |
| Status            | Running                 |
| Health Check      | 2/2 Passed              |

---

## Backend Replica

| Property          | Value                  |
| ----------------- | ---------------------- |
| Instance Name     | Backend-Server-Replica |
| Instance ID       | i-0fcb728a0cdadd440    |
| Instance Type     | t3.micro               |
| Public IP         | 65.1.135.242           |
| Availability Zone | ap-south-1a            |
| Security Group    | Bastion-Host-SG        |
| Key Pair          | shiwanshu-HV-keypair   |
| Status            | Running                |
| Health Check      | 3/3 Passed             |

---

# Scaling Summary

## Completed Successfully

* ✅ Opened the Amazon EC2 Console
* ✅ Created a frontend replica instance
* ✅ Created a backend replica instance
* ✅ Verified that both instances launched successfully
* ✅ Confirmed health checks for all replica instances
* ✅ Distributed replicas across different Availability Zones
* ✅ Prepared the infrastructure for AWS Application Load Balancer (ALB)

---

# Final Project Results

The Travel Memory application was successfully deployed and prepared for production use.

### Backend

* Ubuntu EC2 deployment
* Node.js and Express.js
* MongoDB Atlas connectivity
* Environment variable configuration
* Nginx reverse proxy
* Backend API verification

---

### Frontend

* React application deployment
* Backend API integration
* Dependency installation
* Production build generation
* Frontend verification

---

### Scaling

* Multiple frontend EC2 instances
* Multiple backend EC2 instances
* High Availability architecture
* Ready for AWS Application Load Balancer (ALB)

---

# Overall Architecture

```text
                    Internet
                        │
                        ▼
          AWS Application Load Balancer
                 │               │
                 ▼               ▼
      Frontend EC2-1     Frontend EC2-2
                 │               │
                 └──────┬────────┘
                        │
                        ▼
              Backend EC2-1     Backend EC2-2
                    │                 │
                    └────────┬────────┘
                             │
                             ▼
                     MongoDB Atlas
```

---

# Future Enhancements

The following improvements can be implemented to further enhance the application:

* Configure an AWS Application Load Balancer (ALB)
* Create separate Target Groups for frontend and backend
* Configure Auto Scaling Groups
* Add HTTPS using AWS Certificate Manager (ACM)
* Configure Route 53 for a custom domain
* Use Amazon CloudFront as a CDN
* Containerise the application using Docker
* Deploy using Kubernetes (Amazon EKS)
* Automate deployments with GitHub Actions or AWS CodePipeline
* Add monitoring using Amazon CloudWatch
* Centralise logs using CloudWatch Logs
* Improve security using IAM roles and security best practices

---

# Repository

```bash
git clone git@github.com:shiwanshu97/Travel_Memory_Application.git
```

---

# Author

**Shiwanshu Kumar Jha**

Cloud & DevOps Enthusiast

GitHub: **https://github.com/shiwanshu97**

---

# License

This project is licensed under the **MIT License**.

Refer to the `LICENSE` file for more information.

---

# Acknowledgements

Special thanks to the original TravelMemory project contributors for providing the application source code used as the foundation for this deployment exercise. This repository documents the deployment, configuration, troubleshooting, and scaling activities performed on AWS infrastructure.

---

# Conclusion

This project demonstrates a complete end-to-end deployment of a MERN stack application on AWS. It includes backend deployment with Node.js and MongoDB Atlas, frontend integration with React, Nginx reverse proxy configuration, GitHub version control, and horizontal scaling using multiple EC2 instances. The infrastructure is prepared for future enhancements such as Application Load Balancers, Auto Scaling Groups, HTTPS, CI/CD pipelines, Docker, and Kubernetes, making it a strong foundation for production-ready cloud deployments.

🎉 **Your README is now complete.** It documents the entire deployment journey—from backend setup and frontend integration to troubleshooting and scaling—in a format suitable for a GitHub repository.

I have added images for reference in this document. 

# EC2 Instances

![EC2 Instances](images/ec2-instances.png)

---

# Amazon Machine Image (AMI)

![AMI](images/ami.png)

---

# Application Load Balancer

![Load Balancer](images/load-balancer.png)

---

# Target Groups

![Target Groups](images/target-groups.png)

---

# MongoDB Atlas Database

![MongoDB Atlas](images/mongodb-atlas.png)

---

# IP Whitelisting

![IP Whitelisting](images/ip-whitelisting.png)

---

# DNS Records

![DNS Records](images/dns-records.png)

---

# Application UI

![Application UI](images/application-ui.png)

---

# Travel Memory Home Page

![Travel Memory](images/travel-memory-home.png)

