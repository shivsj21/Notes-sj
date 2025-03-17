# Laravel Artisan Commands

### **General Commands**

- `php artisan --version` - Check your Laravel version. 
- `php artisan list` – Lists all available Artisan commands.  
- `php artisan help [command]` – Shows help for a specific command.  

### **Application Management**
- `php artisan serve` – Runs the application at `http://localhost:8000`.  
- `php artisan down` – Puts the application in maintenance mode.  
- `php artisan up` – Brings the application out of maintenance mode.  

### **Cache & Config Management**
- `php artisan cache:clear` – Clears the application cache.  
- `php artisan config:cache` – Caches the configuration files.  
- `php artisan route:cache` – Caches the routes.  
- `php artisan view:clear` – Clears compiled view files.  

### **Database Management**
- `php artisan migrate` – Runs all pending migrations.  
- `php artisan migrate:rollback` – Rolls back the last batch of migrations.  
- `php artisan migrate:refresh` – Rolls back all migrations and re-runs them.  
- `php artisan db:seed` – Runs database seeders.  
- `php artisan make:migration [name]` – Creates a new migration file.  

###  **Model, Controller, and Resource Generation**
- `php artisan make:model [ModelName]` – Creates a new model.  
- `php artisan make:controller [ControllerName]` – Creates a new controller.  
- `php artisan make:resource [ResourceName]` – Creates a new resource.  

###  **Authentication & Authorization**
- `php artisan make:middleware [MiddlewareName]` – Creates a middleware.  
- `php artisan route:list` – Lists all registered routes.  

###  **Queue & Jobs**
- `php artisan queue:work` – Processes the next job on the queue.  
- `php artisan queue:restart` – Restarts the queue worker.  

###  **Storage Link Creation**
- `php artisan storage:link` – Creates a symbolic link for storage access.  

###  **Testing**
- `php artisan test` – Runs the PHPUnit tests.  
