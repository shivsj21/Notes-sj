# Laravel Apache Setup Guide

This guide outlines the steps to set up a Laravel application on Apache with multiple databases (MySQL and MongoDB), Redis for sessions, Mailgun for email, and Let's Encrypt SSL.

---
## **1. Folder Creation and Permissions:**
```bash
sudo mkdir -p /var/www/html/shivm/test-server-apace/
sudo chown -R www-data:www-data /var/www/html/shivm/test-server-apace/
sudo chmod -R 775 /var/www/html/shivm/test-server-apace/
```
- **Improvement:** Use `www-data:www-data` as the owner for better security with Apache.
- **Tip:** `775` gives write permissions to the group, but in production, consider `755` for increased security.

---
## **2. Git Pull Code:**
```bash
cd /var/www/html/shivm/test-server-apace/
git pull origin main
```
- **Tip:** Use `git fetch --all` and `git reset --hard origin/main` if you want to overwrite local changes (use with caution).

---
## **3. .env Configuration:**
Ensure the `.env` file is set up for:
- **Multiple Databases (MySQL & MongoDB)**
- **Redis Configuration**
- **Mailgun for Emails**

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=your_mysql_database
DB_USERNAME=your_mysql_user
DB_PASSWORD=your_mysql_password

MONGO_DB_CONNECTION=mongodb
MONGO_DB_HOST=127.0.0.1
MONGO_DB_PORT=27017
MONGO_DB_DATABASE=your_mongo_database
MONGO_DB_USERNAME=your_mongo_user
MONGO_DB_PASSWORD=your_mongo_password

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379
SESSION_DRIVER=redis
CACHE_DRIVER=redis

MAIL_MAILER=mailgun
MAILGUN_DOMAIN=your_mailgun_domain
MAILGUN_SECRET=your_mailgun_secret
MAILGUN_ENDPOINT=api.mailgun.net
MAIL_FROM_ADDRESS=your_email@example.com
MAIL_FROM_NAME="${APP_NAME}"
```

---
## **4. HTTP Config (`shivm_apace.conf`):**
```apache
<VirtualHost *:80>
    ServerName apace24.samplejunction.com
    DocumentRoot /var/www/html/shivm/test-server-apace/public/

    <Directory /var/www/html/shivm/test-server-apace/>
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    RewriteEngine on
    RewriteCond %{SERVER_NAME} =apace24.samplejunction.com
    RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]

    Header always set X-Content-Type-Options "nosniff"
    Header always set X-Frame-Options "DENY"
    Header always set X-XSS-Protection "1; mode=block"
</VirtualHost>
```
Enable Headers Module:
```bash
sudo a2enmod headers
sudo systemctl restart apache2
```

---
## **5. Enabling the Site:**
```bash
sudo a2ensite shivm_apace.conf
sudo systemctl reload apache2
```

---
## **6. HTTPS Config (`shivm_apace-le-ssl.conf`):**
```apache
<IfModule mod_ssl.c>
<VirtualHost *:443>
    ServerName apace24.samplejunction.com
    DocumentRoot /var/www/html/shivm/test-server-apace/public

    <Directory /var/www/html/shivm/test-server-apace/>
        AllowOverride All
    </Directory>

    SSLCertificateFile /etc/letsencrypt/live/apace24.samplejunction.com/fullchain.pem
    SSLCertificateKeyFile /etc/letsencrypt/live/apace24.samplejunction.com/privkey.pem
    Include /etc/letsencrypt/options-ssl-apache.conf

    Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains"
</VirtualHost>
</IfModule>
```

---
## **7. Enable the HTTPS Site:**
```bash
sudo a2ensite shivm_apace-le-ssl.conf
sudo systemctl reload apache2
```

---
## **8. SSL Certification:**
```bash
sudo apt update
sudo apt install certbot python3-certbot-apache
sudo certbot --apache -d apace24.samplejunction.com -d www.apace24.samplejunction.com
```

---
## **9. Check Certbot Auto-Renewal:**
```bash
sudo systemctl status certbot.timer
sudo certbot renew --dry-run
```

---
## **10. DNS Configuration:**
- Use:
```bash
curl ifconfig.me
```
- Create `A` records for:
  - `apace24.samplejunction.com`
  - `www.apace24.samplejunction.com`

---
## **Additional Recommendations:**
- Apache Performance: Enable caching modules.
- Laravel Optimization: Use `php artisan config:cache` and related commands.
- File Permissions: Set proper ownership and permissions for storage and cache.
- Firewall Rules: Enable UFW and allow relevant ports.
- Security Hardening: Disable directory listing and hide Apache version.

## **Summary:**
These steps set up a Laravel application with Apache, SSL, Redis, and multiple databases securely and efficiently. Follow the additional recommendations for improved performance and security.

