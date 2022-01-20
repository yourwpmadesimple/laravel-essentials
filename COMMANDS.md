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
```
### web.php
```
Route::get('/rooms', [App\Http\Controllers\ShowRoomsController::class, '__invoke']);
```
### ShowRoomsController MOD 1
```
$rooms = DB::table('rooms')->get();
        if($request->query('id') !== null){
            $rooms = $rooms->where('room_type_id', $request->query('id'));
        }
        return response()->json($rooms);
```

## Resource Controller Action
```
php artisan make:controller BookingController --resource --model=Booking
```
### BookingController.php
```
public function index()
    {
        \DB::table('bookings')->get()->dd();
    }
```
