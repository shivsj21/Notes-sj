# HAProxy SSL Certificate Management Guide

## Commands Explanation

### 1. Stop HAProxy
```bash
systemctl stop haproxy
```
Stops the HAProxy service, likely to free up ports 80 and 443 for Apache to handle SSL certificate renewal.

### 2. Start Apache
```bash
systemctl start apache2
```
Starts the Apache service so that Certbot (Let's Encrypt client) can use it to verify domain ownership.

### 3. Run Certbot for SSL Renewal
```bash
certbot -d samplejunction.com -d www.samplejunction.com
```
Runs Certbot to generate or renew SSL certificates for the specified domains. You must choose an option in the prompt (like 1 or 2), but here it's canceled with `c`.

### 4. Edit Private Key File 
```bash
vi /etc/letsencrypt/live/samplejunction.com/privkey.pem
```
Opens the private key file for editing. The private key is copied from here.

### 5. Edit Certificate File 
```bash
vi /etc/letsencrypt/live/samplejunction.com/fullchain.pem
```
Opens the certificate file where the copied private key is pasted. (ensure that no extra space)

### 6. Stop Apache
```bash
systemctl stop apache2
```
Stops the Apache service to free up ports 80 and 443 for HAProxy to resume its job as the reverse proxy.

### 7. Start HAProxy
```bash
systemctl start haproxy
```
Starts the HAProxy service again to continue serving traffic.

### 8. Check HAProxy Status
```bash
systemctl status haproxy
```
----------------------------------------------------------------------------------------------------------------------
# HAProxy with Let's Encrypt SSL Configuration

## Generating/Renewing Certificates (Using Certbot)

1. **Stop HAProxy (Free up ports 80 & 443):**  
```bash
systemctl stop haproxy
```

2. **Start Apache (For Certbot to Verify Domain):**  
```bash
systemctl start apache2
```

3. **Run Certbot for Certificate Generation/Renewal:**  
```bash
certbot certonly --apache -d samplejunction.com -d www.samplejunction.com
```
This command **only generates the certificate** files, without modifying your Apache config.

4. **Stop Apache:**  
```bash
systemctl stop apache2
```

5. **Start HAProxy:**  
```bash
systemctl start haproxy
```

---

## ✅ Configure HAProxy to Use the Certificates
Let's Encrypt certificates are stored at:  
```
/etc/letsencrypt/live/samplejunction.com/
```
You need to **combine the private key and the fullchain certificate** for HAProxy to use it.  

Create a combined file:  
```bash
cat /etc/letsencrypt/live/samplejunction.com/privkey.pem /etc/letsencrypt/live/samplejunction.com/fullchain.pem > /etc/letsencrypt/live/samplejunction.com/haproxy.pem
```

---

## ✅ Edit HAProxy Configuration File
Open your HAProxy config file (`/etc/haproxy/haproxy.cfg`) and add or update your SSL frontend like this:

```haproxy
frontend https_front
    bind *:443 ssl crt /etc/letsencrypt/live/samplejunction.com/haproxy.pem
    mode http
    option httplog
    default_backend apache_backend
```

---

## ✅ Restart HAProxy to Apply Changes
```bash
systemctl restart haproxy
```

---

## 📌 Automating Certificate Renewal
Let's Encrypt certificates expire every **90 days**. To automate renewal, add this line to your crontab (`crontab -e`):

```bash
0 3 * * * certbot renew --quiet && cat /etc/letsencrypt/live/samplejunction.com/privkey.pem /etc/letsencrypt/live/samplejunction.com/fullchain.pem > /etc/letsencrypt/live/samplejunction.com/haproxy.pem && systemctl reload haproxy
```

This cron job will:
1. **Renew certificates if needed.**  
2. **Update `haproxy.pem` file.**  
3. **Reload HAProxy to apply changes.**  
