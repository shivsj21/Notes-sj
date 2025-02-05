# Mailgun Integration with Laravel

## **Step 1: Create a Mailgun Account**
1. Sign up at [Mailgun](https://www.mailgun.com/).
2. Add your domain in **Sending → Domains**.
3. Verify the domain using DNS records.
4. Get your **Mailgun API Key** and **Domain Name** from the dashboard.

---

## **Step 2: Install Laravel & Dependencies**
Ensure your Laravel project is set up and install the Mailgun driver:

```bash
composer require guzzlehttp/guzzle
```

---

## **Step 3: Configure Mailgun in Laravel**
Edit your `.env` file:

```env
MAIL_MAILER=mailgun
MAILGUN_DOMAIN=your-mailgun-domain.com
MAILGUN_SECRET=your-mailgun-api-key
MAILGUN_ENDPOINT=api.mailgun.net
MAIL_FROM_ADDRESS=no-reply@yourdomain.com
MAIL_FROM_NAME="YourApp Name"
```

Then, update the **mail configuration** in `config/mail.php`:

```php
'mailers' => [
    'mailgun' => [
        'transport' => 'mailgun',
    ],
],
```

Clear the configuration cache:

```bash
php artisan config:clear
```

---

## **Step 4: Set Up Mail Sending**
Use Laravel’s `Mail` facade to send emails.

1. **Create an Email Mailable Class:**
   ```bash
   php artisan make:mail TestMail
   ```

2. **Edit `app/Mail/TestMail.php`:**
   ```php
   namespace App\Mail;

   use Illuminate\Bus\Queueable;
   use Illuminate\Contracts\Queue\ShouldQueue;
   use Illuminate\Mail\Mailable;
   use Illuminate\Queue\SerializesModels;

   class TestMail extends Mailable
   {
       use Queueable, SerializesModels;

       public function build()
       {
           return $this->subject('Test Email')
                       ->view('emails.test'); // Create a Blade file in `resources/views/emails/test.blade.php`
       }
   }
   ```

3. **Send the Email in a Controller:**
   ```php
   use Illuminate\Support\Facades\Mail;
   use App\Mail\TestMail;

   Mail::to('recipient@example.com')->send(new TestMail());
   ```

---

## **Step 5: Test Email Sending**
Run the following command:

```bash
php artisan tinker
```

Then execute:

```php
Mail::to('recipient@example.com')->send(new \App\Mail\TestMail());
```

If everything is configured correctly, you should receive the test email.

---

## **Troubleshooting**
1. **Emails Not Sending?**  
   - Check Mailgun logs in the dashboard.
   - Ensure your domain is verified in Mailgun.
   - Double-check API key and domain in `.env`.

2. **Mailgun in Local Development?**  
   - Mailgun often blocks emails from unverified domains.
   - Use **Mailtrap** for local testing (`MAIL_MAILER=smtp` and `MAIL_HOST=smtp.mailtrap.io`).

---

## **Next Steps**
- Queue emails for better performance (`ShouldQueue` in the Mailable class).
- Use **Mailgun’s EU endpoint** if needed (`MAILGUN_ENDPOINT=api.eu.mailgun.net`).
- Secure your API key with **Laravel Envoy** or environment-specific configs.

---

