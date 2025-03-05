## **1. Linux Commands**  
These are system-level commands used to navigate directories, change permissions, and manage cron jobs.  

### **Directory Navigation (`cd`)**  
- `cd /var/www/html/sumitm/test-server-apace/apace-live/`  
  - Moves into the specified directory.  

### **File & Folder Permissions (`chmod`)**  
- `chmod -R 777 storage/`  
  - Gives **read, write, and execute** permissions to everyone (**rwx-rwx-rwx**) recursively.  
- `chmod -R 777 app/Http/Controllers/Frontend/Auth/ConfirmAccountController.php`  
  - Changes permission for a specific file.  

### **Cron Jobs (`crontab`)**  
- `crontab -l`  
  - Lists all cron jobs.  
- `crontab -e`  
  - Opens the crontab file for editing.  

### **Running Scheduled Tasks**  
- `php artisan schedule:run`  
  - Runs Laravel's scheduled tasks (used in cron jobs).  

---

## **2. Git Commands**  
These commands are used for version control.  

### **Checking Branches**  
- `git branch`  
  - Lists all available branches.  
- `git checkout dev`  
  - Switches to the **dev** branch.  
- `git checkout -b anil_sjpl348_28Nov`  
  - Creates a new branch and switches to it.  

### **Adding & Committing Changes**  
- `git add .`  
  - Stages all modified files for commit.  
- `git commit -m 'fix hindi feedback points'`  
  - Commits changes with a message.  

### **Pushing & Pulling Code**  
- `git pull`  
  - Fetches the latest changes from the remote repository.  
- `git push --set-upstream origin anil_sjpl348_28Nov`  
  - Pushes the branch to the remote repository and sets the upstream tracking.  

### **Merging & Resolving Conflicts**  
- `git merge anil_sjpl344_hindibugs`  
  - Merges another branch into the current branch.  
- `git merge --abort`  
  - Cancels a merge in case of conflicts.  

---

## **3. Laravel Artisan Commands**  
These are Laravel-specific commands.  

### **Clearing Config & Cache**  
- `php artisan config:cache`  
  - Clears and refreshes the configuration cache.  
- `php artisan view:clear`  
  - Clears compiled Blade templates.  

### **Managing Logs**  
- `chmod -R 777 storage/logs/`  
  - Gives full permission to log files.  

### **Running Laravel Jobs & Queues**  
- `php artisan schedule:run`  
  - Runs scheduled tasks like email notifications, database cleanups, etc.  

---
Here's an explanation of the commands used:

### Navigation & Listing  
- `cd <directory>`: Change directory to the specified path.  
- `ll`: List files and directories in the current directory with detailed information (alias for `ls -l`).

### Permissions & Ownership  
- `chmod -R 777 <path>`: Recursively change permissions to read, write, and execute for all users. **(Not recommended for security reasons)**.  
- `chown <user>:<group> <file/dir>`: Change the owner and group of a file or directory.  
- `sudo usermod -a -G <group> <user>`: Add a user to a group.

### Apache Configuration  
- `vi /etc/apache2/sites-enabled/<file>`: Edit Apache virtual host configuration files.  
- `sudo apachectl configtest`: Check Apache configuration for syntax errors.  
- `systemctl restart apache2.service`: Restart the Apache service.

### Laravel Commands  
- `php artisan schedule:run`: Run scheduled tasks defined in Laravel's `App\Console\Kernel.php`.  
- `php artisan <command>`: Run a Laravel-specific Artisan command, e.g., `RepDataAPI:sync_projects`.

### Log Management  
- `tail -100 /var/log/syslog`: View the last 100 lines of the system log.  
- `tail -f /storage/logs/laravel.log`: Continuously view the end of a Laravel log file.  
- `rm <file>`: Remove (delete) a file.

### Crontab (Scheduled Tasks)  
- `crontab -e`: Edit the cron jobs for the current user.  
- `crontab -L`: (Typo, should be `crontab -l`) List cron jobs.  
- `crontab -i`: Confirm before deleting a cron job.

### Miscellaneous  
- `history`: Show a list of recently executed commands.  
- `clear`: Clear the terminal screen.  
- `groups <user>`: List the groups a user is a member of.  
- `id <user>`: Display user and group IDs for a user.  
- `grep <pattern> /etc/group`: Search for a pattern (e.g., `www-data`) in the group file.
