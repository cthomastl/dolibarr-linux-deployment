Dolibarr ERP: Migration from Docker to Native LAMP Stack
Project Overview
This project documents the strategic migration of a Dolibarr ERP/CRM instance from a containerized Docker environment to a high-performance, native LAMP (Linux, Apache, MariaDB, PHP) stack on Ubuntu Server. By moving away from Docker, the architecture allows for granular database tuning, direct filesystem management, and optimized system resource allocation.

Phase 1: Containerized Proof-of-Concept
Initially, the application was deployed via Docker to establish a rapid baseline for testing and configuration.

Deployment: Utilized docker run -d -p 8080:80 --name dolibarr dolibarr/dolibarr to initialize the service.

Networking: Configured port mapping to bridge internal container port 80 to host port 8080.

Diagnostics: Verified connectivity using ping and ip addr to map the Docker bridge gateway and ensure host-to-container communication.

Phase 2: Native LAMP Stack Implementation
To achieve enterprise-grade control, the environment was rebuilt natively on Ubuntu Server.

1. The Stack
Web Server: Apache2 with optimized VirtualHost configurations.

Database: MariaDB for relational data storage.

Runtime: PHP 8.x with critical extensions like php-mysqli, php-gd, and php-curl for ERP functionality.

2. Database Hardening and Configuration
Manual SQL configuration was performed to resolve authentication conflicts and enforce the principle of least privilege:

SQL

CREATE DATABASE dolibarr;
CREATE USER 'dolibarr_user'@'localhost' IDENTIFIED BY 'password123';
GRANT ALL PRIVILEGES ON dolibarr.* TO 'dolibarr_user'@'localhost';
FLUSH PRIVILEGES;
3. Filesystem Security and Permissions
Managed Linux ownership to allow the www-data service to interact with the application while maintaining security:

Path: /var/www/html/dolibarr

Storage: Created a secure document root at /var/www/html/dolibarr/documents.

Permissions Lifecycle: Implemented chmod 666 during the initial setup phase to allow configuration writing, then hardened the directory to chmod 444 for production read-only security.

Phase 3: Identity and Access Management (IAM)
A core component of this project involved configuring Linux user permissions to allow delegated administration.

Case Study: Delegated Admin "James"
User Creation: Provisioned a new system user "James" for server-side maintenance.

Access Validation: Verified SSH/Local login capabilities for the new user.

Privilege Escalation: Identified initial permission gaps where "James" lacked administrative rights.

Resolution: Modified sudoers or group memberships to grant "James" the necessary permissions to manage other system users.

Technical Evidence
Network Security
Configured UFW (Uncomplicated Firewall) to allow inbound traffic on port 80. <img width="941" height="448" alt="UFW Firewall Status" src="https://github.com/user-attachments/assets/04e58eca-d66d-457b-a36b-4712ed1fe070" />

User Onboarding and Access
Provisioning the new administrator and verifying login integrity. <img width="935" height="404" alt="Creating User James" src="https://github.com/user-attachments/assets/2b065ed4-8b97-4a14-802b-0cf852b15a5b" />

<img width="944" height="437" alt="Successful Login Verification" src="https://github.com/user-attachments/assets/7b0c0d37-8558-48f7-bae6-b003fb328433" />

Permission Management
Demonstrating the transition from restricted access to full administrative delegation. <img width="945" height="440" alt="Access Denied Evidence" src="https://github.com/user-attachments/assets/802c8928-977e-430b-b647-ab48ebef725e" />

<img width="950" height="407" alt="Admin Rights Granted" src="https://github.com/user-attachments/assets/07d724a3-da05-4447-be1c-ec7b29fce059" />

<img width="950" height="440" alt="James Adding Users Successfully" src="https://github.com/user-attachments/assets/2772e564-c870-4c5b-8ed2-c2217363c709" />

Skills Demonstrated
System Administration: Linux CLI, Permissions (chmod/chown), SSH, User Management.

DevOps and Infrastructure: Docker Networking, Port Mapping, Migration Strategy.

Database Admin: MariaDB/MySQL Management, SQL User Permissions.

Security: UFW Firewall Configuration, Directory Hardening, RBAC (Role-Based Access Control).
