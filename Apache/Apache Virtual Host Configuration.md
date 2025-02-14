# Apache Virtual Host Configuration Explained

## **VirtualHost Block**
```apache
<VirtualHost *:80>
```
- Defines a virtual host that listens on port **80** (HTTP).
- `*` means it applies to all IP addresses on the server.

## **Server Admin & Domain Settings**
```apache
ServerAdmin admin@yourdomain.com
```
- Email for the server administrator (displayed in error messages).

```apache
ServerName yourdomain.com
ServerAlias www.yourdomain.com
```
- `ServerName` specifies the primary domain.
- `ServerAlias` allows alternative domain names (e.g., `www.yourdomain.com`).

## **Document Root**
```apache
DocumentRoot /var/www/html/yourdomain.com/public
```
- Defines the root directory for the website files.

## **Directory Permissions**
```apache
<Directory /var/www/html/yourdomain.com/public>
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
</Directory>
```
- `<Directory>` configures access for the document root.
- `Options Indexes FollowSymLinks`:  
  - `Indexes`: Allows directory listing if no `index.html` is found.  
  - `FollowSymLinks`: Allows symbolic links to be followed.
- `AllowOverride All`: Enables `.htaccess` files to override settings.
- `Require all granted`: Grants access to all users.

## **Logging**
```apache
ErrorLog ${APACHE_LOG_DIR}/yourdomain_error.log
CustomLog ${APACHE_LOG_DIR}/yourdomain_access.log combined
```
- `ErrorLog`: Stores error messages.
- `CustomLog`: Logs all access requests in a **combined** format (IP, request, response, etc.).

## **SSL Virtual Host Block**
```apache
<IfModule mod_ssl.c>
<VirtualHost *:443>
    ServerAdmin admin@yourdomain.com
    ServerName yourdomain.com
    ServerAlias www.yourdomain.com
    DocumentRoot /var/www/html/yourdomain.com/public

    <Directory /var/www/html/yourdomain.com/public>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    SSLEngine on
    SSLCertificateFile /etc/letsencrypt/live/yourdomain.com/fullchain.pem
    SSLCertificateKeyFile /etc/letsencrypt/live/yourdomain.com/privkey.pem

    ErrorLog ${APACHE_LOG_DIR}/yourdomain_ssl_error.log
    CustomLog ${APACHE_LOG_DIR}/yourdomain_ssl_access.log combined
</VirtualHost>
</IfModule>
```
- `<IfModule mod_ssl.c>`: Ensures SSL module is enabled before applying SSL settings.
- `VirtualHost *:443>`: Configures the virtual host to listen on **port 443** (HTTPS).
- `SSLEngine on`: Enables SSL encryption.
- `SSLCertificateFile`: Specifies the SSL certificate file.
- `SSLCertificateKeyFile`: Specifies the SSL private key file.
- Separate **error and access logs** for SSL.

## **Closing Tag**
```apache
</VirtualHost>
</IfModule>
```
- Ends the virtual host and SSL module block.

This setup ensures secure HTTPS access with an SSL certificate from Let's Encrypt.

