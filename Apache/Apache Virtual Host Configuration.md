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

## **Closing Tag**
```apache
</VirtualHost>
```
- Ends the virtual host block.

This setup is essential for hosting a website with Apache, defining where files are stored, access rules, and logging. 🚀

