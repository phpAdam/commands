# php artisan

First, there is a command **php artisan list** which gives us all the commands, like this:

```php
  make:channel         Create a new channel class
  make:command         Create a new Artisan command
  make:controller      Create a new controller class
  make:event           Create a new event class
  make:exception       Create a new custom exception class
  make:factory         Create a new model factory
  make:job             Create a new job class
  make:listener        Create a new event listener class
  make:mail            Create a new email class
  make:middleware      Create a new middleware class
  make:migration       Create a new migration file
  make:model           Create a new Eloquent model class
  make:notification    Create a new notification class
  make:observer        Create a new observer class
  make:policy          Create a new policy class
  make:provider        Create a new service provider class
  make:request         Create a new form request class
  make:resource        Create a new resource
  make:rule            Create a new validation rule
  make:seeder          Create a new seeder class
  make:test            Create a new test class
```

# 1. make:controller
This command creates a new controller file in app/Http/Controllers folder.

### Example usage:

```php
php artisan make:controller UserController
```

### Parameters:

```php
--resource
```

The controller will contain a method for each of the available resource operations – index(), create(), store(), show(), edit(), update(), destroy().

```php
--api
```

Similar to –resource above, but generate only 5 methods: index(), store(), show(), update(), destroy(). Because create/edit forms are not needed for API.
```php
--invokable
```

Generates controller with one __invoke() method. Read more about invokable controllers here.

```php
--model=Photo
```

If you are using route model binding and would like the resource controller’s methods to type-hint a model instance.

```php
--parent=Photo
```

Officially undocumented parameter, in the code it says “Generate a nested resource controller class” but for me it failed to generate a Controller properly. So probably work in progress.

# 2. make:model
Create a new Eloquent model class.

### Example usage:

```php
php artisan make:model Photo
```

### Parameters:

```php
--migration
```
or

```php
-m
```
Create a new migration file for the model.

```php
--controller
```

or

```php
-c
```
Create a new controller for the model.

```php
--resource
```
or
```php
-r
```
Indicates if the generated controller should be a resource controller.

Yes, you’ve got it right, you can do it like this:
```php
php artisan make:model Project --migration --controller --resource
```
Or even shorter:

```php
php artisan make:model Project -mcr
```
But that’s not all to make:model.
```php
--factory
```
or
```php
-f
```
Create a new factory for the model.
```php
--all
```
or
```php
-a
```
Generate all of the above: a migration, factory, and resource controller for the model.

And even that’s not all.

```php
--force
```
Create the class even if the model already exists.
```php
--pivot
```
Indicates if the generated model should be a custom intermediate table model.

# 3. make:migration
Create a new migration file.

### Example usage:
```php
php artisan make:migration create_projects_table
```
### Parameters:
```php
--create=Table
```
The table to be created.
```php
--table=Table
```
The table to migrate.
```php
--path=Path
```
The location where the migration file should be created.
```php
--realpath
```
Indicate any provided migration file paths are pre-resolved absolute path.
```php
--fullpath
```
Output the full path of the migration.

# 4. make:seeder
Create a new database seeder class.

### Example usage:
```php
php artisan make:seeder BooksTableSeeder
```
### Parameters: none.

```php
5. make:request
```
Create a new form request class in app/Http/Requests folder.

### Example usage:
```php
php artisan make:request StoreBlogPost
```
### Parameters: none.

# 6. make:middleware
Create a new middleware class.

### Example usage:
```php
php artisan make:middleware CheckAge
```
### Parameters: none.

# 7. make:policy
Create a new policy class.

### Example usage:
```php
php artisan make:policy PostPolicy
```
### Parameters:
```php
--model=Photo
```
The model that the policy applies to.

# 8. make:command
Create a new Artisan command.

### Example usage:
```php
php artisan make:command SendEmails
```
### Parameters:
```php
--command=Command
```
The terminal command that should be assigned.

# 9. make:event
Create a new event class.

### Example usage:
```php
php artisan make:event OrderShipped
```
### Parameters: none.

# 10. make:job
Create a new job class.

### Example usage:
```php
php artisan make:job SendReminderEmail
```
### Parameters:
```php
--sync
```
Indicates that job should be synchronous.

# 11. make:listener
Create a new event listener class.

### Example usage:
```php
php artisan make:listener SendShipmentNotification 
```
### Parameters:
```php
--event=Event
```
The event class being listened for.
```php
--queued
```
Indicates the event listener should be queued.

# 12. make:mail
Create a new email class.

### Example usage:
```php
php artisan make:mail OrderShipped
```
### Parameters:
```php
--markdown
```
Create a new Markdown template for the mailable.
```php
--force
```
Create the class even if the mailable already exists.

# 13. make:notification
Create a new notification class.

### Example usage:
```php
php artisan make:notification InvoicePaid
```
### Parameters:
```php
--markdown
```
Create a new Markdown template for the notification.
```php
--force
```
Create the class even if the notification already exists.

# 14. make:provider
Create a new service provider class.

### Example usage:
```php
php artisan make:provider DuskServiceProvider
```
### Parameters: none.

# 15. make:test
Create a new test class.

### Example usage:
```php
php artisan make:test UserTest
```
### Parameters:
```php
--unit
```
Create a unit (or, otherwise, feature) test.

# 16. make:channel
Create a new channel class for broadcasting.

### Example usage:
```php
php artisan make:channel OrderChannel
```
### Parameters: none.

# 17. make:exception
Create a new custom exception class.

### Example usage:
```php
php artisan make:exception UserNotFoundException
```
### Parameters:
```php
--render
```
Create the exception with an empty render method.
```php
--report
```
Create the exception with an empty report method.

# 18. make:factory
Create a new model factory.

### Example usage:
```php
php artisan make:factory PostFactory --model=Post
```
### Parameters:
```php
--model=Post
```
The name of the model.

# 19. make:observer
Create a new observer class.

### Example usage:
```php
php artisan make:observer PostObserver --model=Post
```
### Parameters:
```php
--model=Post
```
The model that the observer applies to.

# 20. make:rule
Create a new validation rule.

### Example usage:
```php
php artisan make:rule Uppercase
```
### Parameters: none.

# 21. make:resource
Create a new API resource.

### Example usage:
```php
php artisan make:resource PostResource
```
### Parameters:
```php
--collection=Post
```
Create a ResourceCollection instead of individual Resource class.