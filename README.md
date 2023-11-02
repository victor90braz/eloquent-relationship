I've updated the README to include the latest code snippets and examples. The README now provides a comprehensive guide for understanding and using the Eloquent relationships and database query logging in your Laravel project. You can use this updated README for your project:

````markdown
# Eloquent Relationship Demo

This repository demonstrates various Eloquent relationships in Laravel, including one-to-one, one-to-many, many-to-many, has-many-through, and polymorphic relationships. It provides examples and usage instructions for each relationship type.

## Table of Contents

-   [Relationship Types](#relationship-types)
-   [Setup](#setup)
-   [Usage](#usage)
    -   [Create a Profile Schema and Migrate](#create-a-profile-schema-and-migrate)
    -   [Get a User's Profile](#get-a-users-profile)
-   [DB Query Logging](#db-query-logging)

## Relationship Types

This project illustrates the following Eloquent relationship types:

-   One-to-One
-   One-to-Many
-   Many-to-Many
-   Has-Many-Through
-   Polymorphic Relations

## Setup

To set up this project, follow these steps:

1. Clone this repository to your local environment:

    ```shell
    git clone https://github.com/victor90braz/eloquent-relationship.git
    ```

2. Navigate to the project directory:

    ```shell
    cd eloquent-relationship
    ```

3. Install the required dependencies using Composer:

    ```shell
    composer install
    ```

4. Create a copy of the `.env` file and configure your database connection settings:

    ```shell
    cp .env.example .env
    ```

5. Generate an application key:

    ```shell
    php artisan key:generate
    ```

6. Migrate the database to create the necessary tables:

    ```shell
    php artisan migrate
    ```

## Usage

### Create a Profile Schema and Migrate

Before demonstrating the relationships, you need to create a `profile` schema and migrate it to the database. To do this, follow these steps:

1. Create a migration for the `Profile` model:

    ```shell
    php artisan make:migration create_profiles_table
    ```

2. Open the newly created migration file at `database/migrations/yyyy_mm_dd_create_profiles_table.php` and define the schema for the `profiles` table.

3. Run the migration to create the `profiles` table:

    ```shell
    php artisan migrate
    ```

### Get a User's Profile

You can retrieve a user's profile using Laravel's Eloquent relationships. Here's an example of how to do it:

1. Start a Tinker session:

    ```shell
    php artisan tinker
    ```

2. Create a new `User` instance:

    ```php
    $user = new User();
    ```

3. Retrieve a user's profile by specifying the user's ID:

    ```php
    $profile = $user->find(2)->profile;
    ```

4. You can also log the SQL queries executed by the application using the following code:

    ```php
    DB::listen(function ($sql) {
        var_dump($sql->sql, $sql->bindings);
    });
    ```

    This will help you see the SQL queries generated by Eloquent.

For more detailed examples and usage of each relationship type, please refer to the provided code in this repository.

## DB Query Logging

To enable database query logging and see the SQL queries that are executed, you can use the `DB::listen` function. You can add the following code to your Tinker session or other parts of your Laravel application:

```php
DB::listen(function ($sql) {
    var_dump($sql->sql, $sql->bindings);
});
```
````

This will log the SQL queries and their bindings for debugging and analysis purposes.

---

# Second Way to Log

You can also log SQL queries using the `DB::enableQueryLog` and `DB::getQueryLog` methods in your Tinker session. Here's how to do it:

```php
> DB::enableQueryLog();
> = null

> $profile = $user->find(2);
> string(52) "select * from `users` where `users`.`id` = ? limit 1"
> array(1) {
> [0]=>
> int(2)
> }
> = App\Models\User {#7114
> ...
```

To view the logged queries, you can use the following code:

```php
> DB::getQueryLog();
> = [
>     [
>         "query" => "select * from `users` where `users`.`id` = ? limit 1",
>         "bindings" => [
>             2,
>         ],
>         "time" => 1.03,
>     ],
>     // Other logged queries
> ]
```

This provides an alternative way to log SQL queries for debugging purposes.

# Next Tinker Example

You can also use Tinker to interact with your models and relationships. Here's an example:

```shell
$ php artisan tinker
Psy Shell v0.11.22 (PHP 8.2.10 — cli) by Justin Hileman

> $user = new User();
[!] Aliasing 'User' to 'App\Models\User' for this Tinker session.
= App\Models.User {#7095}

> $user->first()
= App.Models.User {#7097
    id: 1,
    username: "admin",
    name: "admin",
    email: "admin@gmail.com",
    email_verified_at: null,
    #password: "$2y$10$2Us440ufiOTCfxbEBjNW5O9u8gG5zDegNtE3/hHwrXSuPnZacrjUe",
    #remember_token: null,
    created_at: "2023-11-02 16:52:17",
    updated_at: "2023-11-02 16:52:17",
  }

> $user->experience;
= null

> $user->find(1)->experience


= App.Models.Experience {#7108
    id: 1,
    user_id: 1,
    points: 145,
    created_at: "2023-11-02 17:48:36",
    updated_at: "2023-11-02 17:48:36",
  }
```

This demonstrates how you can use Tinker to access your models and relationships interactively for testing and debugging.

```

```
