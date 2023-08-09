# Laravel Developer Test - Home Task README

This project leverages Laravel for backend functionality and employs PHPUnit for testing, while integrating Vue3 and TailwindCSS for frontend design. The main features include:

### Basic Authentication and User Roles
The project offers basic Laravel authentication with a Vue-based administrator login. This enables users to log in as administrators.

### Database Setup and Seeding
The application employs database migrations to create the necessary schemas for two main entities: Companies and Employees. The Companies table comprises fields such as Name (required), email, and logo (minimum 100×100), and website. Meanwhile, the Employees table includes fields like First name (required), last name (required), Company (linked through a foreign key to Companies), email, and phone. The initial setup involves the creation of a seeder using the command `php artisan make:seeder DatabaseSeeder`, followed by populating the database with sample data through `php artisan db:seed --class=DatabaseSeeder`.

### File Storage
Logos for the companies are stored in the `storage/app/public` directory, which is made accessible from the public domain. This is facilitated by establishing a storage link with the command `php artisan storage:link`.

### Resource Controllers and CRUD Operations
The project employs Laravel's resource controllers to manage CRUD (Create / Read / Update / Delete) operations for both Companies and Employees. The controllers come with default methods: index, create, store, edit, update, and destroy. Laravel's validation functions are used in conjunction with Request classes to ensure data integrity.

### Pagination
Laravel's built-in pagination is utilized to display lists of Companies and Employees, with each page showing up to 10 entries.

### Custom Authentication
Authentication mechanisms are developed without relying on Laravel Fortify, enhancing the project's uniqueness.

### Email Notifications
The application incorporates email notifications, which are triggered when new company entries are added. For email testing, Mailtrap is employed with the sender set as `markdv39@gmail.com` and the receiver as the current user's email.

### Testing
PHPUnit is used for testing purposes, with the project configured to work with Mailtrap for email-related tests.

### Instructions for Running:
1. Execute the following commands:
2. Create a seeder using: `php artisan make:seeder DatabaseSeeder`
3. Seed the database using: `php artisan db:seed --class=DatabaseSeeder`
4. Establish a storage link with: `php artisan storage:link`
5. Launch the project by executing `php artisan serve`.

For questions or assistance, contact `markdv39@gmail.com`.
