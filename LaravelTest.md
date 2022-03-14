# Laravel Test

### Testing Tools

- PHPunit, Mockery, PHPSpec & Storyplayer
- Laravel has PHPunit integrated

### What is PHPunit?

Framework independent library that can be used for unit testing.

### When to use PHPunit?
- Crawling your site's URL
- Submitting forms
- Checking status codes

### Some important terms

- Unit test - Will verify that individual units of code work as expected
- Features test - Tests the way individual units work toghether and pass message
- Regression tests - You're going describle exactly what a user should be able to do
- HTTP tests Allows you to make simple HTTP request(GET,POST,PUT,PATCH,DELETE)
- Authenticating Responses - Application tests in authentication and authorization
- Database test - Tools and assetions to make it easier to test database driven apps

### Create & Running the test

Create `Feature` test
```php
php artisan make:test UserTest
```

Create `Unit` test
```php
php artisan make:test UserTest --unit
```

Run your test
```php
php artisan test
```

## HTTP Tests

 Laravel provides a fluent API for making HTTP request
 
 5 calls you can make
 ```php
$this->get($url, $header=[])
$this->post($url, $data, $header=[])
$this->put($url, $data, $header=[])
$this->patch($url, $data, $header=[])
$this->delete($url, $data, $header=[])
```

- You need to return a response object
- This is not illuminate response but an instance of the TestResponse
- Wrapper around the Response object with additional assertions
- 40+ avaiable assertions

```php
// HTTP Test
public function test_it_stores_new_users()
{
    $response = $this->post('/register', [
        'name' => 'admin',
        'email' => 'admin@gmail.com',
        'password' => 'admin1234',
        'password_confirmation' => 'admin1234'
    ]);

    $response->assertRedirect('/home');
}
```


## Database Test
- Two primary assertions

```php
$this->assertDatabaseHas()
$this->assertDatabaseMissing()
```

### $this->assertDatabaseHas()

How does this look in SQL?
- Perform a SQL WHERE statment
- You pass in data, looks in the DB for a match

```php
    // Database test
    public function test_database_has()
    {
        $this->assertDatabaseHas('users', [
            'name'=> 'admin'
        ]);
    }

    // Database test
    public function test_database_missing()
    {
        $this->assertDatabaseMissing('users', [
            'name'=> 'admin1'
        ]);
    }
```

## Seeder Tests

First we need to create 
```php
php artisan make:seeder UsersTableSeeder
```

Next, fill this up
```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\Hash;
use Illuminate\Support\Facades\DB;

class UsersTableSeeder extends Seeder
{
    public function run()
    {
        DB::table('users')->insert([
            'name' => 'admin1',
            'email' => 'admin1@gmail.com',
            'password' => Hash::make('password')
        ]);
    }
}
```
Add this Seeder Class to `DatabaseSeeder`
```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;

class DatabaseSeeder extends Seeder
{
    public function run()
    {
        // \App\Models\User::factory(10)->create();
        $this->call(UsersTableSeeder::class);
    }
}
```
We can use this seeder
```php
php artisan db:seed --class=UsersTableSeeder
//or
php artisan migrate:fresh --seed
```

This will execute seeder and will check if we have correct inserting

```php
    // Test Seeders
    public function test_if_seeders_works()
    {
        $this->seed(); // Seed all seeders in the Seeders folder
        // php artisan db:seed
    }
```

Now, we can run our test
```php
php artisan test
```
