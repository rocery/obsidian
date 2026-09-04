Install:
composer create-project laravel/laravel:^12.0 nama-app
composer create-project laravel/laravel nama-app -> Latest  Version Laravel

Create New DB for Login Management:
CREATE DATABASE db_users CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

Edit config/database.php
Add new Database config, example:
```
'users_db' => [
	'driver' => 'mysql',
	'host' => env('USERS_DB_HOST', '127.0.0.1'),
	'port' => env('USERS_DB_PORT', '3306'),
	'database' => env('USERS_DB_DATABASE', 'db_users'),
	'username' => env('USERS_DB_USERNAME', 'root'),
	'password' => env('USERS_DB_PASSWORD', ''),
	'unix_socket' => env('DB_SOCKET', ''),
	'charset' => 'utf8mb4',
	'collation' => 'utf8mb4_unicode_ci',
	'prefix' => '',
	'prefix_indexes' => true,
	'strict' => true,
	'engine' => null,
	'options' => extension_loaded('pdo_mysql') ? array_filter([
	Mysql::ATTR_SSL_CA => env('MYSQL_ATTR_SSL_CA'),
		]) : [],
],
```

Check db,
```
php artisan tinker
DB::connection('db_users')->getDatabaseName();
DB::connection('iot')->getDatabaseName();
```

Make migration for db_users
```
php artisan make:migration create_users_table

Isi: database/migration/file_migration
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema; 

return new class extends Migration
{
	protected $connection = 'db_users';
	public function up(): void
	{
		Schema::connection('db_users')->create('users', function (Blueprint $table) {
			$table->id();
			$table->string('name');
			$table->string('email')->unique();
			$table->timestamp('email_verified_at')->nullable();
			$table->string('password');
			$table->rememberToken();
			$table->timestamps();
		});
	}
	
	/**
	* Reverse the migrations.
	*/
	public function down(): void
	{
		Schema::dropIfExists('db_users');
	}
};
```

Make migration for session
```
php artisan make:migration create_sessions_table

Isi:
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    protected $connection = 'users_db';

    public function up(): void
    {
        Schema::connection('users_db')->create('sessions', function (Blueprint $table) {
            $table->string('id')->primary();
            $table->foreignId('user_id')->nullable()->index();
            $table->string('ip_address', 45)->nullable();
            $table->text('user_agent')->nullable();
            $table->text('payload');
            $table->integer('last_activity')->index();
        });
    }

    public function down(): void
    {
        Schema::connection('users_db')->dropIfExists('sessions');
    }
};
```

