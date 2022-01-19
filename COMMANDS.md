# Laravel Commands

## Run this to get into MYSQL CLI
```
sudo su

cd /var/lib/mysql

```

## Database Commands
```
SHOW Databases;

USE [Database name]; e.g USE homestead;

SHOW TABLES; to see all tables

SELECT * from [table]; e.g select * from users
```

## Create Migrations
```
php artisan make:migration create_hotel_tables --create=rooms

php artisan migrate (executes any code changes in files)
```
