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

### 4. Edit Private Key File (Not Recommended for Direct Editing)
```bash
vi /etc/letsencrypt/live/samplejunction.com/privkey.pem
```
Opens the private key file for editing. The private key is copied from here.

### 5. Edit Certificate File (Not Recommended for Direct Editing)
```bash
vi /etc/letsencrypt/live/samplejunction.com/fullchain.pem
```
Opens the certificate file where the copied private key is pasted (though this is not the correct process; private keys shouldn't be placed in the fullchain file).

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

