# PHP Signup Form with MariaDB on AWS EC2

A complete end-to-end 3-tier web application deployment on AWS EC2. The application collects user inputs through a web frontend, processes the submission using PHP, and permanently stores records in a MariaDB database server.

📌 Project Overview

This project demonstrates the complete deployment cycle of a dynamic web application hosted on an AWS Cloud instance. It highlights server configuration, database schema design, web server setup (Nginx / Apache), and Git/GitHub code management workflow.

Deployment Environment: AWS EC2 (Linux)

Web Server: Nginx / Apache

Backend Processing: PHP

Database Management System: MariaDB (Database: FCT, Table: users)

Frontend: HTML5 / CSS3

Version Control: Git & GitHub

 # 🏗️ Architecture & Workflow Diagram

flowchart LR
    A[Developer / Local] -->|Push Code| B(GitHub Repository)
    B -->|Deploy / Upload| C[AWS EC2 Linux Server]
    D[User / Browser] -->|1. Open Form via Public IP| E[Web Server Nginx / Apache]
    E -->|2. Run PHP Script| F[PHP Application]
    F -->|3. Database Query| G[(MariaDB Database: FCT)]
    G -->|4. Return Data| F
    F -->|5. Display Success Page| D


 # 🔁 Project Execution Flow:

Form Access: The user opens signup.html via the EC2 Public IP (http://<EC2-PUBLIC-IP>/php_project/signup.html).

Data Submission: The user fills in the details (Name, Email, Website, Comment, Gender) and submits the form.

PHP Processing: The web server forwards the POST request to submit.php.

Database Insertion: PHP connects to MariaDB and executes an INSERT SQL statement into the users table of the FCT database.

Confirmation Page: On successful insertion, a confirmation message ("New record created successfully!") is displayed along with the submitted summary.

🗄️ Database Schema & Data Verification

1. Table Structure (FCT.users)

Field
Type
Null
Key
Default
Extra
id
int(11)
NO
PRI
NULL
auto_increment
name
varchar(50)
YES
NULL
email
varchar(50)
YES
NULL
website
varchar(50)
YES
NULL
comment
varchar(50)
YES
NULL
gender
varchar(20)
YES
NULL

 ## 2. Live Database Verification Screenshot

💻 Screenshots & Application Interface

📥 1. User Signup Interface (signup.html)

📤 2. Form Submission Output (submit.php)

⚙️ Deployment & Setup Instructions

Step 1: Server Preparation & Package Installation

Update system repositories and install the LEMP/LAMP stack packages:

# For RHEL / Amazon Linux / Fedora
sudo dnf update -y
sudo dnf install -y nginx mariadb-server php php-fpm php-mysqlnd git

# Enable and start required services
sudo systemctl enable --now nginx mariadb php-fpm


Step 2: MariaDB Database Setup

Access the database command-line tool and create the required schema:

sudo mysql -u root -p


Execute the following SQL commands:

CREATE DATABASE FCT;
USE FCT;

CREATE TABLE users (
  id INT(11) NOT NULL AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(50),
  email VARCHAR(50),
  website VARCHAR(50),
  comment VARCHAR(50),
  gender VARCHAR(20)
);

-- Verify structure
DESC users;
EXIT;


Step 3: Application Code Deployment

Clone or copy your project files into the web root directory:

# Navigate to web root
cd /var/www/html/

# Clone repository or copy project folder
sudo git clone https://github.com/your-username/php_project.git

# Set permissions for web server
sudo chown -R nginx:nginx /var/www/html/php_project
sudo chmod -R 755 /var/www/html/php_project

# Restart services
sudo systemctl restart nginx php-fpm


🚀 Future Roadmap & Best Practices

[ ] Security Enhancements: Implement prepared statements (PDO / mysqli) to guard against SQL Injection vulnerabilities.

[ ] Cloud Managed DB: Migrate local MariaDB to an AWS RDS (Relational Database Service) instance.

[ ] SSL Encryption: Configure HTTPS using Let's Encrypt certificates via Certbot.

[ ] Automated CI/CD: Implement GitHub Actions pipeline for automated testing and continuous deployment on push.

👤 Author

Tushar Thorat
