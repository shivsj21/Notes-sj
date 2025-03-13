### 1. Max Connections (MySQL)
To check the current value of maximum connections allowed by MySQL, run:
```sql
SHOW VARIABLES LIKE 'max_connections';
```

### 2. Max Memory Limit (PHP)
To check the current memory limit set in PHP, use:
- **From Command Line:**  
```bash
php -i | grep memory_limit
```
- **From PHP Script:**  
```php
<?php
    echo ini_get('memory_limit');
?>
```

### 3. Max Execution Time (PHP)
To check the current max execution time for PHP scripts, use:
- **From Command Line:**  
```bash
php -i | grep max_execution_time
```
- **From PHP Script:**  
```php
<?php
    echo ini_get('max_execution_time');
?>
```



