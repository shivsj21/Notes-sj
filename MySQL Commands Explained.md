# MySQL Commands Explained

## **User & Privileges Management**

### **Granting Privileges**  
```sql
GRANT ALL PRIVILEGES ON database_name.* TO 'username'@'localhost' WITH GRANT OPTION;
```
- Grants all privileges on a specific database to a user.
- `WITH GRANT OPTION` allows the user to grant privileges to others.

### **Revoking Privileges**  
```sql
REVOKE ALL PRIVILEGES ON database_name.* FROM 'username'@'localhost';
```
- Removes all privileges from a specific user on a database.

### **Flushing Privileges**  
```sql
FLUSH PRIVILEGES;
```
- Reloads the privilege tables to apply changes made to user permissions.

### **Showing Grants for a User**  
```sql
SHOW GRANTS FOR 'username'@'localhost';
```
- Displays the privileges granted to a specific user.

### **Listing Users**  
```sql
SELECT user, host FROM mysql.user;
```
- Lists all MySQL users and their associated hosts.

## **Database & Table Management**

### **Showing Available Databases**  
```sql
SHOW DATABASES;
```
- Lists all databases on the MySQL server.

### **Using a Specific Database**  
```sql
USE database_name;
```
- Switches to a specific database.

### **Showing Tables in a Database**  
```sql
SHOW TABLES;
```
- Lists all tables within the selected database.

### **Dropping a Database**  
```sql
DROP DATABASE database_name;
```
- Deletes a database permanently.

## **Backup & Restore**

### **MySQL Dump (Backup a Database)**  
```sql
mysqldump -u username -p database_name > /path/to/backup.sql
```
- Creates a backup of a database and saves it as a `.sql` file.

## **Server Variables & Configuration**

### **Checking Max Connections**  
```sql
SHOW VARIABLES LIKE "max_connections";
```
- Displays the current max connections allowed by MySQL.

### **Setting Max Connections**  
```sql
SET GLOBAL max_connections = 200;
```
- Increases or decreases the maximum allowed MySQL connections.

### **Checking MySQL Port & Hostname**  
```sql
SHOW VARIABLES WHERE Variable_name = 'port';
SHOW VARIABLES WHERE Variable_name = 'hostname';
```
- Displays the MySQL server’s port and hostname.

## **Process & Performance**

### **Showing Running Processes**  
```sql
SHOW PROCESSLIST;
```
- Displays currently running queries and connections.

### **Checking Active Database**  
```sql
SELECT DATABASE();
```
- Returns the name of the currently selected database.
