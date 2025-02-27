This document explains the server setup used in your organization, hosted on DigitalOcean, using the following stack:

- **Ubuntu** as the operating system
- **Apache** as the web server
- **PHP** as the server-side scripting language
- **MongoDB** and **MySQL** as the databases

## Why is it Called LAMP?
The stack resembles the traditional **LAMP** architecture:
- **L**inux (Operating System) – In this case, Ubuntu
- **A**pache (Web Server)
- **M**ySQL (Database) – Although MongoDB is also used
- **P**HP (Programming Language)

However, since your organization uses **Laravel**, a PHP framework, the stack is commonly referred to as **Laravel** instead of LAMP.

## Why Laravel?
Your team refers to it as **Laravel** because Laravel is the PHP framework powering your application. It enhances the basic LAMP stack with features like:
- **MVC Architecture**: Organizes code into Models, Views, and Controllers for better maintainability
- **Eloquent ORM**: Simplifies database interactions with an intuitive syntax
- **Routing**: Manages URLs and endpoints more efficiently
- **Blade Templating**: Helps create dynamic web pages with reusable components
- **Built-in Security**: Protection against common web vulnerabilities

## Summary
- **LAMP** describes the underlying infrastructure (Linux, Apache, MySQL/MongoDB, PHP).
- **Laravel** is the framework built on top of this stack, enhancing productivity and maintainability.

While the infrastructure is technically LAMP, it's more accurate to call it **Laravel** in your context because it's the framework powering the application logic.

