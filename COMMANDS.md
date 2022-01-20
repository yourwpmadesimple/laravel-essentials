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

## Seeding
```
php artisan db:seed
```

## Controllers
```
php artisan make:controller ShowRoomsContoller --invokable
```
### ShowRoomsController
```
return response('A list of rooms', 200);
Route::get('/rooms', [App\Http\Controllers\ShowRoomsController::class, '__invoke']); -> web.php
```

