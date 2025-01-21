# Laravel-Site-Deployment-on-aaPanel


This guide explains how to deploy a Laravel application on aaPanel, a free and open-source hosting control panel.




## Prerequisites
1. A server with aaPanel installed.
2. A domain or subdomain configured to point to your server's IP.
3. Basic knowledge of SSH and command-line tools.


## Step 1: Set Up the Environment
1. Login to aaPanel:
  Access aaPanel via http://your-server-ip:8888.
  Use your admin credentials to log in.
  Install Required Software:

2. Go to the App Store in aaPanel.
  Install:
  1. PHP (recommended: 8.x)
  2. MySQL
  3. Nginx or Apache (choose your preferred web server)
  4. Composer
  5. Redis (optional, if your Laravel app uses it)
  6. Memcached
  7.<img width="1691" alt="Image" src="https://github.com/user-attachments/assets/25147771-6d00-4cf7-8da0-c4bcedc17054" />


## Step 2: Create a New Website
1. Navigate to Websites in the aaPanel dashboard.
2. Click Add Site.
3. Domain: Enter your domain or subdomain.
4. Root Directory: Set it to /www/wwwroot/your-domain.
5. PHP Version: Select the installed PHP version (e.g., 8.1).
6. Install the relevant extensions. <img width="792" alt="Image" src="https://github.com/user-attachments/assets/32594e80-6746-4ffc-8b0a-4e169af56b04" />
7. In addition there are configurations that need to be done on the php app FPM Profile as seen below
   <img width="1709" alt="Image" src="https://github.com/user-attachments/assets/ccb47be7-f531-4665-ab8c-91c049da6c6b" />




## Step 3: Upload Laravel Files
1. Via File Manager:
Go to the File Manager in aaPanel.
Navigate to /www/wwwroot/your-domain.
Upload your Laravel project (as a ZIP file) and extract it.

2. Via SSH (Optional):
Use an SFTP client like FileZilla or an SSH terminal.
Run the following commands:
cd /www/wwwroot/your-domain
git clone https://github.com/your-repository.git .







## Step 4: Set Up Laravel
1. Open the terminal in aaPanel or SSH into your server.
cd /www/wwwroot/your-domain
composer install
2. Install node. Remember to change the version of the node.js that matches the one used for development.
3. <img width="1718" alt="Image" src="https://github.com/user-attachments/assets/b95c8fc5-7f31-495c-9e04-1a33369a4241" />
4. Set Permissions:
chmod -R 755 "storage"
chmod -R 755 "bootstrap/cache"
5. Set Up the Environment File:
    Copy the .env.example file to .
    Update database credentials, app URL, and other configurations in the .env file.
    










## Step 5: Configure the Web Server
Nginx Configuration
1. Go to Websites > Domain > Config.
2. Update the root directory to Laravel's public folder:
    root /www/wwwroot/your-domain/public;
    index index.php index.html;
    
3. Add the following Nginx rules for Laravel:
       location / {
                 try_files $uri $uri/ /index.php?$query_string;
         }
   




## Step 6: Configure SSL 
1. Go to SSL in aaPanel.
2. Issue a free Let's Encrypt certificate for your domain.
3. Force HTTPS redirection in your web server settings.
