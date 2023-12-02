# মডিউল ১০ এর এসাইনমেন্ট
## Laravel Practice Assignment
### Tasks:
#### Task 01:
1. Create a new Laravel project named "MigrationAssignment" using the Laravel command-line interface.
```shell
composer create-project laravel/laravel MigrationAssignment
cd MigrationAssignment
php artisan migrate
php artisan serve
```
Note: Edit .env file. `DB_DATABASE=MigrationAssignment`

#### Task 02:
1. Within the project, create a new migration file named "create_products_table" that will be responsible for creating a table called "products" in the database. The "products" table should have the following columns:
- id: an auto-incrementing integer and primary key.
- name: a string column to store the product name.
- price: a decimal column to store the product price.
- description: a text column to store the product description.
- created_at: a timestamp column to store the creation date and time.
- updated_at: a timestamp column to store the last update date and time.

```shell
php artisan make:migration create_products_table
```

Note: Edit  `2023_12_02_062055_create_products_table.php` file
```php
Schema::create('products', function (Blueprint $table) {
    $table->id();
    $table->string('name', 50);
    $table->double('price', 10, 2);
    $table->text('description');
    $table->timestamp('created_at')->useCurrent();
    $table->timestamp('updated_at')->useCurrent()->useCurrentOnUpdate();
});
```
#### Task 03:
After creating the migration file, run the migration to create the "products" table in the database.
```shell
php artisan migrate
```

#### Task 04:
Modify the existing migration file "create_products_table" to add a new column called "quantity" to the "products" table. The "quantity" column should be an integer column and allow null values.
```shell
php artisan migrate:rollback
```

Edit the Edit  `2023_12_02_062055_create_products_table.php` file
```php
Schema::create('products', function (Blueprint $table) {
    $table->id();
    $table->string('name', 50);
    $table->double('price', 10, 2);
    $table->integer('quantity')->nullable();
    $table->text('description');
    $table->timestamp('created_at')->useCurrent();
    $table->timestamp('updated_at')->useCurrent()->useCurrentOnUpdate();
});
```

#### Task 05:
Create a new migration file named "add_category_to_products_table" that will be responsible for adding a new column called "category" to the "products" table. The "category" column should be a string column with a maximum length of 50 characters.
```shell
php artisan make:migration add_category_to_products_table
```

Edit the `2023_12_02_064718_add_category_to_products_table.php` file
```php
public function up(): void
{
    Schema::table('products', function (Blueprint $table) {
        $table->string('category', 50);
    });
}

public function down(): void
{
    Schema::table('products', function (Blueprint $table) {
        $table->dropColumn('category');
    });
}
```

#### Task 06:
After creating the new migration file, run the migration to add the "category" column to the "products" table.
```shell
php artisan migrate
```

#### Task 07:
Create a new migration file named "create_orders_table" that will be responsible for creating a table called "orders" in the database. The "orders" table should have the following columns:
- id: an auto-incrementing integer and primary key.
- product_id: an unsigned integer column to establish a foreign key relationship with the "id" column of the "products" table.
- quantity: an integer column to store the quantity of products ordered.
- created_at: a timestamp column to store the creation date and time.
- updated_at: a timestamp column to store the last update date and time.

```shell
php artisan make:migration create_orders_table
```

Edit the `2023_12_02_065452_create_orders_table.php` file
```php
Schema::create('orders', function (Blueprint $table) {
    $table->id();
    $table->unsignedBigInteger('product_id');
    $table->foreign('product_id')->references('id')->on('products')->restrictOnDelete()->cascadeOnUpdate();
    $table->integer('quantity');
    $table->timestamp('created_at')->useCurrent();
    $table->timestamp('updated_at')->useCurrent()->useCurrentOnUpdate();
});
```

#### Task 08:
```shell
php artisan migrate
```

