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
