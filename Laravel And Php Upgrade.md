# Laravel 5.7.28 to 11 & PHP 7.2 to 8 Upgrade Guide

## Step 1: Backup Your Application

1. **Backup Code**: Copy your Laravel app directory to another location.
2. **Backup Database**:

```bash
mysqldump -u your_user -p your_database_name > backup.sql
```

---

## Step 2: Update PHP Version (To PHP 8.2)

1. **Add PHP PPA Repository** (If not already added):

```bash
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
```

2. **Install PHP 8.2 and Required Extensions**:

```bash
sudo apt-get install php8.2 php8.2-cli php8.2-fpm php8.2-mysql php8.2-xml php8.2-mbstring php8.2-zip php8.2-curl
```

3. **Disable Old PHP Version and Enable New One**:

```bash
sudo a2dismod php7.2
sudo a2enmod php8.2   
sudo systemctl restart apache2
```

4. **Check PHP Version**:

```bash
php -v
```

---

## Step 3: Update Composer

1. **Update Composer to Latest Version**:

```bash
composer self-update
```

---

## Step 4: Update Laravel Application

1. **Navigate to Your Project Directory**:

```bash
cd /var/www/html/obhi/sjpanel.com/public_html/sjpanel-live/
```

2. **Update **``** File**:

```json
"require": {
    "php": "^8.2",
    "laravel/framework": "^11.0"
}
```

3. **Update Dependencies**:

```bash
composer update
```

---

## Step 5: Update Laravel Codebase

1. **Review and Update Any Deprecated Code**.
2. **Update Configuration Files**:

```bash
php artisan config:clear
php artisan cache:clear
php artisan route:clear
php artisan view:clear
```

---

## Step 6: Database Migration (If Needed)

If you have migrations to run:

```bash
php artisan migrate
```

---

## Step 7: Deploy Laravel Application

1. **Set Permissions**:

```bash
sudo chown -R www-data:www-data /var/www/html/obhi/sjpanel.com/public_html/sjpanel-live/
sudo chmod -R 775 /var/www/html/obhi/sjpanel.com/public_html/sjpanel-live/storage
sudo chmod -R 775 /var/www/html/obhi/sjpanel.com/public_html/sjpanel-live/bootstrap/cache
```

2. **Restart Apache**:

```bash
sudo systemctl restart apache2
```

---

## Step 8: Test Your Application

- Visit your application URL to confirm it's working properly.
- Check logs for any errors:

```bash
tail -f /var/log/apache2/error.log
```

