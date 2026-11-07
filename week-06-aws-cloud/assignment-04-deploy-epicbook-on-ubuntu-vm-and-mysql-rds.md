# Assignment 4 — Deploy EpicBook on Ubuntu VM + MySQL RDS with Secure Cloud Network

<<<<<<< HEAD
Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI
=======
Part of the DevOps Micro Internship (DMI) with Agentic AI
>>>>>>> upstream/main

---

## Purpose

In this assignment, you will deploy the EpicBook web application in AWS using a secure two-tier architecture: an Ubuntu EC2 instance with Nginx in a public subnet, and a private MySQL RDS database with restricted security-group access. The completed deployment must prove that the frontend, backend, and private database communicate successfully end to end.

---

# Task 1 — Create VPC + Public/Private Subnets + Routing

## Goal

<<<<<<< HEAD
Create `epicbook-vpc` (10.0.0.0/16) with a public subnet (10.0.1.0/24) and a private subnet (10.0.2.0/24), attach an Internet Gateway, and route only the public subnet to it.
=======
Create the AWS network for the EpicBook deployment with a public subnet for the EC2 instance and private subnets for Amazon RDS MySQL.
>>>>>>> upstream/main

### Evidence

#### Screenshot 1 — VPC details showing CIDR 10.0.0.0/16

<<<<<<< HEAD
![alt text](<screenshots/Screenshot_1-assig_4_1.png>)

#### Screenshot 2 — Subnets list showing both subnets and their CIDRs

![alt text](<screenshots/Screenshot_2_assig_4_1.png>)

#### Screenshot 3 — Route table showing 0.0.0.0/0 → IGW and association with the public subnet

![alt text](<screenshots/Screenshot_3_assig_4_1.png>)
=======
Add your screenshot here.

---

#### Screenshot 2 — Subnets list showing the public subnet and both private database subnets with their CIDR ranges.

Add your screenshot here.

---

#### Screenshot 3 — Route table showing 0.0.0.0/0 → IGW and association with the public subnet

Add your screenshot here.

---
>>>>>>> upstream/main

# Task 2 — Create Security Groups (EC2 + RDS) with Least Privilege

## Goal

<<<<<<< HEAD
Create `epicbook-ec2-sg` (SSH from your IP, HTTP/HTTPS public) and `epicbook-rds-sg` (MySQL 3306 only from `epicbook-ec2-sg`).
=======
Create security groups that allow users to access the EpicBook application while restricting database access to the EC2 instance.
>>>>>>> upstream/main

### Evidence

#### Screenshot 4 — EC2 security-group inbound rules showing ports and sources

<<<<<<< HEAD
![alt text](<screenshots/Screenshot_4_assig_4_2.png>)

#### Screenshot 5 — RDS security-group inbound rule showing MySQL 3306 allowed from the EC2 security group

![alt text](<screenshots/Screenshot_5_assig_4_2.png>)
=======
Add your screenshot here.

---

#### Screenshot 5 — RDS security-group inbound rule showing MySQL 3306 allowed from the EC2 security group

Add your screenshot here.

---
>>>>>>> upstream/main

# Task 3 — Launch Ubuntu EC2 in Public Subnet

## Goal

<<<<<<< HEAD
Launch an Ubuntu 20.04 instance in the public subnet with `epicbook-ec2-sg` attached, and connect to it over SSH.
=======
Launch the EC2 instance that will host the EpicBook application and connect to it through SSH.
>>>>>>> upstream/main

### Evidence

#### Screenshot 6 — EC2 instance summary showing the public IPv4 address, subnet, and security group

<<<<<<< HEAD
![alt text](<screenshots/Screenshot_6_assig_4_3.png>)

#### Screenshot 7 — Terminal showing a successful SSH login with the `ubuntu@...` prompt

![alt text](<screenshots/Screenshot_7_assig_4_3.png>)
=======
Add your screenshot here.

---

#### Screenshot 7 — Terminal showing a successful SSH login with the `ubuntu@...` prompt

Add your screenshot here.

---
>>>>>>> upstream/main

# Task 4 — Install Required Software on EC2

## Goal

<<<<<<< HEAD
Install Node.js, npm, Nginx, and the MySQL client on the instance, and confirm Nginx is running.
=======
Prepare Ubuntu to download and run EpicBook, receive HTTP traffic, and connect to RDS.
>>>>>>> upstream/main

### Evidence

#### Screenshot 8 — Output of `node -v` and `npm -v`

<<<<<<< HEAD
![alt text](<screenshots/Screenshot_8_assig_4_4.png>)

#### Screenshot 9 — Output of `systemctl status nginx`

![alt text](<screenshots/Screenshot_9_assig_4_4.png>)

#### Screenshot 10 — Output of `mysql --version`

![alt text](<screenshots/Screenshot_10_assig_4_4.png>)
=======
Add your screenshot here.

---

#### Screenshot 9 — Output of `systemctl status nginx`

Add your screenshot here.

---

#### Screenshot 10 — Output of `mysql --version`

Add your screenshot here.

---
>>>>>>> upstream/main

# Task 5 — Create RDS MySQL in Private Subnet (No Public Access)

## Goal

<<<<<<< HEAD
Create a private MySQL RDS instance in `epicbook-vpc` using a DB Subnet Group over the private subnet, with `epicbook-rds-sg` attached and public access disabled.
=======
Launch a private MySQL database accessible only from the application EC2 security group.
>>>>>>> upstream/main

### Evidence

#### Screenshot 11 — RDS instance summary showing Publicly accessible: No

<<<<<<< HEAD
![alt text](<screenshots/Screenshot_11_assig_4_5.png>)

#### Screenshot 12 — Connectivity & security section showing the VPC and attached security group

![alt text](<screenshots/Screenshot_12_assig_4_5.png>)
=======
Add your screenshot here.

---

#### Screenshot 12 — Connectivity & security section showing the VPC and attached security group

Add your screenshot here.

---
>>>>>>> upstream/main

# Task 6 — Initialize Database (SQL Dump Import)

## Goal

<<<<<<< HEAD
Connect to RDS from EC2, create the `epicbook` database, and import the provided SQL dump.
=======
Download EpicBook and populate bookstore with the schema, authors, and books required by the application.
>>>>>>> upstream/main

### Evidence

#### Screenshot 13 — Terminal showing successful `SHOW TABLES;` output with tables listed

<<<<<<< HEAD
![alt text](<screenshots/Screenshot_13_assig_4_6.png>)
=======
Add your screenshot here.

---
>>>>>>> upstream/main

# Task 7 — Deploy EpicBook Backend and Configure Environment Variables

## Goal

<<<<<<< HEAD
Clone the EpicBook repository, install backend dependencies, configure `.env` with the RDS endpoint and credentials, and start the backend on port 3000.
=======
Run EpicBook on port 8080 and connect its Sequelize models to bookstore in RDS.
>>>>>>> upstream/main

### Evidence

#### Screenshot 14 — Terminal showing the repository cloned and the `ls` output

<<<<<<< HEAD
![alt text](<screenshots/Screenshot_14_assig_4_7.png>)

#### Screenshot 15 — Terminal showing the backend running, or `ss -tulpn` showing the port open

![alt text](<screenshots/Screenshot_15_assig_4_7.png>)

#### Screenshot 16 — `curl` output proving the backend responds; a 200, 301, or 404 response is acceptable if the service responds

![alt text](<screenshots/Screenshot_16_assig_4_7.png>)

# Task 8 — Serve Frontend Using Nginx + Reverse Proxy to Backend

## Goal

Copy the frontend files to the Nginx web root and configure Nginx to reverse-proxy `/api/` to the Node backend.
=======
Add your screenshot here.

---

#### Screenshot 15 — Terminal showing EpicBook running, or ss -tulpn output showing port 8080 listening

Add your screenshot here.

---

#### Screenshot 16 — `curl` output proving the backend responds; a 200, 301, or 404 response is acceptable if the service responds

Add your screenshot here.

---

# Task 8 — Configure Nginx as a Reverse Proxy and Enable Persistence.

## Goal

Expose EpicBook through Nginx on port 80 and keep its Node.js process running after SSH disconnects and server reboots.
>>>>>>> upstream/main

### Evidence

#### Screenshot 17 — `nginx -t` success output

<<<<<<< HEAD
![alt text](<screenshots/Screenshot_17_assig_4_8.png>)

#### Screenshot 18 — Nginx configuration snippet showing the `/api/` reverse proxy

![alt text](<screenshots/Screenshot_18_assig_4_8.png>)
=======
Add your screenshot here.

---

#### Screenshot 18 — Nginx configuration snippet showing location / forwarding requests to http://127.0.0.1:8080

Add your screenshot here.

---
>>>>>>> upstream/main

# Task 9 — End-to-End Testing (Frontend ↔ Backend ↔ RDS)

## Goal

<<<<<<< HEAD
Verify the frontend loads publicly, the backend responds through Nginx, and EC2 can query the private RDS database.
=======
Verify the public application and its use of the imported RDS data.
>>>>>>> upstream/main

### Evidence

#### Screenshot 19 — Browser showing the EpicBook application loaded with the public IP visible

<<<<<<< HEAD
![alt text](<screenshots/Screenshot_19_assig_4_9.png>)

#### Screenshot 20 — Terminal showing a successful API call through the public endpoint, such as `curl http://<EC2_PUBLIC_IP>/api/...`

![alt text](<screenshots/Screenshot_20_assig_4_9.png>)

#### Screenshot 21 — Terminal showing the successful database connectivity test using `SELECT 1;` or similar

![alt text](<screenshots/Screenshot_21_assig_4_9.png>)

=======
Add your screenshot here.

---

#### Screenshot 20 — Terminal showing a successful HTTP request to EpicBook through the public Nginx endpoint using curl -i http://<EC2_PUBLIC_IP>/

Add your screenshot here.

---

#### Screenshot 21 — Terminal showing the successful database connectivity test using `SELECT 1;` or similar

Add your screenshot here.

---

# LinkedIn Post (Required)

## Goal

Publish a LinkedIn post sharing your experience deploying EpicBook on an Ubuntu EC2 instance with Nginx and a private Amazon RDS MySQL database.

Include:
- A screenshot of the live EpicBook application showing the book listing
- Your application URL: `http://<EC2_PUBLIC_IP>/`
- A caption in your own words explaining what you deployed, how the main components connect, and what you learned about network security, Nginx, and PM2
- One challenge you faced and how you resolved it, if applicable

Include these hashtags:

#DMIByPravinMishra #AWS #DevOps #CloudComputing

Add the credit note for your track, replace `YOUR-GITHUB-USERNAME` with your GitHub username, and include the tags specified in the assignment guidelines.

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`Add your URL here`

---

#### Screenshot 22 — Published LinkedIn post showing your caption, application URL, and live EpicBook screenshot

Add your screenshot here.

> **Privacy Note:** Do not expose passwords, private keys, `.env` values, database credentials, or sensitive AWS account information.

---

# Submission Instructions

- Add all required screenshots in your submission
- Do not expose PEM contents, passwords, `.env` values, or other secrets

---

# Completion Checklist

- [ ] Task 1: VPC, public/private subnets, IGW, and public routing created (Screenshots 1–3)
- [ ] Task 2: Least-privilege EC2 and RDS security groups created (Screenshots 4–5)
- [ ] Task 3: Ubuntu EC2 launched in the public subnet with SSH verified (Screenshots 6–7)
- [ ] Task 4: Node.js, npm, Nginx, and MySQL client, Git installed (Screenshots 8–10)
- [ ] Task 5: Private MySQL RDS created with no public access (Screenshots 11–12)
- [ ] Task 6: Database initialized from the SQL dump (Screenshot 13)
- [ ] Task 7: Backend deployed and responding on port 8080 (Screenshots 14–16)
- [ ] Task 8: Nginx proxying requests to EpicBook, with PM2 persistence. (Screenshots 17–18)
- [ ] Task 9: Frontend, backend, and RDS verified end to end (Screenshots 19–21)
- [ ] No sensitive data exposed
- [ ] LinedIn post published

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) — Agentic AI Track.*
>>>>>>> upstream/main
