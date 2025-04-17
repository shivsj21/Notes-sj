1st step
   Hosting server/webserver => apache/nginx
   Database mssql/postgress/ mysql /mongo

2nd step
   Code git pull

3rd step
   server useage
   code base
   database connect => which fie include => connection string -> database dump or existing database

4th
   Application step up

   directory and codebase

   existing database or new database 
   assign new users

   give permission

   webserver and dbserver

   make a config file with ssl without ssl  domain name , web directory, ssl certificate location, private key

   webserver ready
   db server ready
   apche configuration ready


   DNS entry  done

-------------------------------------------------------------------------------------------------



# Setting Up Laravel with Apache, MySQL, MongoDB, Redis, and SSL

## Step 1: Create and Set Up the Project Directory

1. Create a directory for the project:
   ```bash
   sudo mkdir -p /var/www/html/shivm/test-server-apace/
   ```
2. Set proper ownership to `www-data` for security:
   ```bash
   sudo chown -R www-data:www-data /var/www/html/shivm/test-server-apace/
   ```
3. Set proper permissions:
   ```bash
   sudo chmod -R 775 /var/www/html/shivm/test-server-apace/
   ```

## Step 2: Pull the Project Code

Navigate to the project directory and pull the latest code from the repository:

```bash
cd /var/www/html/shivm/test-server-apace/
git pull origin main  # Adjust branch name as necessary
```

## Step 3: Configure the Environment File

Modify the `.env` file to set up necessary configurations:

- Database connections (MySQL & MongoDB)
- Redis for session handling
- Mailgun for sending emails

```bash
vim .env  # Edit and update configuration
```

## Step 4: Configure Apache for HTTP

1. Create and edit the Apache configuration file:
   ```bash
   sudo vim /etc/apache2/sites-available/shivm_apace.conf
   ```
2. Add the following configuration:
   ```apache
   <VirtualHost *:80>
       ServerName apace24.samplejunction.com
       ServerAdmin YourEmail@YourDomain.com
       DocumentRoot /var/www/html/shivm/test-server-apace/public/

       <Directory /var/www/html/shivm/test-server-apace/>
           AllowOverride All
       </Directory>

       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined

       RewriteEngine on
       RewriteCond %{SERVER_NAME} =apace24.samplejunction.com
       RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
   </VirtualHost>
   ```

## Step 5: Enable the Site and Reload Apache

```bash
sudo a2ensite shivm_apace.conf
sudo systemctl reload apache2
```

## Step 6: Configure Apache for HTTPS (1st perform step 8 -le-ssl.conf file automatically created and skip step 6 and 7)

1. Create and edit the SSL configuration file:
   ```bash
   sudo vim /etc/apache2/sites-available/shivm_apace-le-ssl.conf
   ```
2. Add the following configuration:
   ```apache
   <IfModule mod_ssl.c>
   <VirtualHost *:443>
       ServerName apace24.samplejunction.com
       ServerAdmin YourEmail@YourDomain.com
       DocumentRoot /var/www/html/shivm/test-server-apace/public

       <Directory /var/www/html/shivm/test-server-apace/>
           AllowOverride All
       </Directory>

       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined

       SSLCertificateFile /etc/letsencrypt/live/apace24.samplejunction.com/fullchain.pem
       SSLCertificateKeyFile /etc/letsencrypt/live/apace24.samplejunction.com/privkey.pem
       Include /etc/letsencrypt/options-ssl-apache.conf
   </VirtualHost>
   </IfModule>
   ```

## Step 7: Enable the SSL Site and Reload Apache

```bash
sudo a2ensite shivm_apace-le-ssl.conf
sudo systemctl reload apache2
```

## Step 8: Generate an SSL Certificate Using Certbot

Run the following command to obtain an SSL certificate:

```bash
sudo certbot --apache -d apace24.samplejunction.com
```

## Step 9: Verify Certbot Auto-Renewal

Check if Certbot auto-renewal is active:

```bash
sudo systemctl status certbot.timer
```

## Step 10: Update DNS Records

1. Get the server’s public IP:
   ```bash
   curl ifconfig.me
   ```
2. Add an A record in your domain's DNS settings, pointing `apace24.samplejunction.com` to the retrieved public IP address.

## Step 11: Set Permissions for Laravel Storage and Cache

To ensure Laravel has proper write access:

```bash
sudo chown -R www-data:www-data /var/www/html/shivm/test-server-apace/storage /var/www/html/shivm/test-server-apace/bootstrap/cache
sudo chmod -R 775 /var/www/html/shivm/test-server-apace/storage /var/www/html/shivm/test-server-apace/bootstrap/cache
```

---

### Your Laravel application with Apache, MySQL, MongoDB, Redis, and SSL is now fully set up!

