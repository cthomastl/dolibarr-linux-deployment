# dolibarr-linux-deployment

Dolibarr ERP: Migration from Docker to Native LAMP Stack
This project documents the process of deploying and migrating the Dolibarr ERP/CRM from a containerized Docker environment to a native Linux, Apache, MariaDB, and PHP (LAMP) stack on Ubuntu Server.

1. Initial Docker Deployment
Originally, the application was deployed using Docker to ensure a quick startup.

Command used: docker run -d -p 8080:80 --name dolibarr dolibarr/dolibarr

Networking: Configured port mapping to expose the internal container port 80 to the host port 8080.

Troubleshooting: Verified connectivity using ping and ip addr to identify the host IP  and the Docker bridge gateway

2. Transition to Manual LAMP Stack
To gain more control over the database and filesystem, I migrated to a native installation.

OS: Ubuntu Server

Web Server: Apache2

Database: MariaDB

Language: PHP 8.x with required extensions (php-mysqli, php-gd, php-curl, etc.)

3. Database Configuration
Configured the MariaDB backend manually via the command line to resolve authentication conflicts:

SQL

CREATE DATABASE dolibarr;
CREATE USER 'dolibarr_user'@'localhost' IDENTIFIED BY 'password123';
GRANT ALL PRIVILEGES ON dolibarr.* TO 'dolibarr_user'@'localhost';
FLUSH PRIVILEGES;
4. Filesystem & Permissions
Managed Linux permissions to allow the webserver (www-data) to write the configuration and store documents.

Path: /var/www/html/dolibarr

Documents: Created a secure directory at /var/www/html/dolibarr/documents.

Permissions Fix: Resolved "File not writable" errors during installation using chmod 666 for setup and reverting to chmod 444 for production security.

5. Network Security
Configured UFW (Uncomplicated Firewall) to allow inbound traffic on port 80.


 <img width="941" height="448" alt="image" src="https://github.com/user-attachments/assets/04e58eca-d66d-457b-a36b-4712ed1fe070" />

  Skills Demonstrated


System Administration: Linux CLI, Permissions Management, SSH.

DevOps: Docker Networking, Port Mapping, Container lifecycle.

Database Admin: SQL User/Grant management, MariaDB troubleshooting.

Web Development: Apache VirtualHost concepts, PHP environment tuning.


Created User James
<img width="935" height="404" alt="image" src="https://github.com/user-attachments/assets/2b065ed4-8b97-4a14-802b-0cf852b15a5b" />

James tries to login to the server
<img width="944" height="437" alt="image" src="https://github.com/user-attachments/assets/7b0c0d37-8558-48f7-bae6-b003fb328433" />
James is able to log in to the server

<img width="945" height="440" alt="image" src="https://github.com/user-attachments/assets/802c8928-977e-430b-b647-ab48ebef725e" />
As you can see James doesnt have permissions, lets add those
<img width="950" height="407" alt="image" src="https://github.com/user-attachments/assets/07d724a3-da05-4447-be1c-ec7b29fce059" />
James can now add users himself
<img width="950" height="440" alt="image" src="https://github.com/user-attachments/assets/2772e564-c870-4c5b-8ed2-c2217363c709" />



