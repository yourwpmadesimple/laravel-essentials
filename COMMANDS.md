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

## Index Action
```
public function index()
    {
        $bookings = DB::table('bookings')->get();
        return view('bookings.index')->with('bookings', $bookings);
    }
```

## index.blade.php
```
@extends('layouts.app')

@section('buttons')
<a class="btn btn-primary" href="{{ route('bookings.create') }}" role="button">Add New Booking</a>
@endsection

@section('content')
<table class="table">
    <thead>
        <tr>
            <th>ID</th>
            <th>Room</th>
            <th>Start Date</th>
            <th>End Date</th>
            <th>Reservation?</th>
            <th>Paid?</th>
            <th>Started?</th>
            <th>Passed?</th>
            <th>Created</th>
            <th class="Actions">Actions</th>
        </tr>
    </thead>
    <tbody>
        @forelse ($bookings as $booking)
            <tr>
                <td>{{ $booking->id }}</td>
                <td>{{ $booking->room_id }}</td>
                <td>{{ date('F d, Y', strtotime($booking->start)) }}</td>
                <td>{{ date('F d, Y', strtotime($booking->end)) }}</td>
                <td>{{ $booking->is_reservation ? 'Yes' : 'No' }}</td>
                <td>{{ $booking->is_paid ? 'Yes' : 'No' }}</td>
                <td>{{ (strtotime($booking->start) < time()) ? 'Yes' : 'No' }}</td>
                <td>{{ (strtotime($booking->end) < time()) ? 'Yes' : 'No' }}</td>
                <td>{{ date('F d, Y', strtotime($booking->created_at)) }}</td>
                <td class="actions">
                    <a
                        href="{{ action('BookingController@show', ['booking' => $booking->id]) }}"
                        alt="View"
                        title="View">
                      View
                    </a>
                    <a
                        href="{{ action('BookingController@edit', ['booking' => $booking->id]) }}"
                        alt="Edit"
                        title="Edit">
                      Edit
                    </a>
                </td>
            </tr>
        @empty
        @endforelse
    </tbody>
</table>
@endsection
```

### Create action for BookingController
```
public function create()
    {
        $users = DB::table('users')->get()->pluck('name', 'id')->append('none')->dd();
        $rooms = DB::table('rooms')->get()->pluck('name', 'id');
        return view('bookins.create')
            ->with('users', $users)
            ->with('rooms', $rooms);
    }
```
