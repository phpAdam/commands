# Raw Database Queries in Laravel

## 1. Most Typical: selectRaw() with Avg/Sum/Count Calculations
If you need to perform groupBy() and then use some aggregation function from MySQL, like AVG() or COUNT(), it’s useful to perform a Raw Query for that specific section.

Example from Laravel documentation:
```php
$users = DB::table('users')
    ->selectRaw('count(*) as user_count, status')
    ->where('status', '<>', 1)
    ->groupBy('status')
    ->get();
```
Another example:
```php
$products = DB::table('products')
    ->leftjoin('category','category.product_id','=','products.id')
    ->selectRaw('COUNT(*) as nbr', 'products.*')
    ->groupBy('products.id')
    ->get();
```
Another example – we can even perform avg() and count() in the same statement.
```php
$salaries = DB::table('salaries')
    ->selectRaw('companies.name as company_name, avg(salary) as avg_salary, count(*) as people_count')
    ->join('companies', 'salaries.company_id', '=', 'companies.id')
    ->groupBy('companies.id')
    ->orderByDesc('avg_salary')
    ->get();
```
## 2. Filtering YEARS: groupByRaw, orderByRaw and havingRaw
What if you want to add some SQL calculations inside of “group by” or “order by”?
We have methods like groupByRaw() and orderByRaw() for this. Also, we can use additional “where” statement after grouping, by “having” SQL statement with havingRaw().

For example, how to group by a YEAR of a certain date/time field?
```php
$results = User::selectRaw('YEAR(birth_date) as year, COUNT(id) as amount')
    ->groupByRaw('YEAR(birth_date)')
    ->havingRaw('YEAR(birth_date) > 2000')
    ->orderByRaw('YEAR(birth_date)')
    ->get();
```
## 3. Calculating one field with sub-query: selectRaw()
If you want to return one specific column as a calculation from other columns, and you want that calculation to happen in SQL query, here’s how it can look:
```php
$products = Product::select('id', 'name')
    ->selectRaw('price - discount_price AS discount')
    ->get();
```
Another example – CASE statement of SQL:
```php
$users = DB::table('users')
    ->select('name', 'surname')  
    ->selectRaw("(CASE WHEN (gender = 1) THEN 'M' ELSE 'F' END) as gender_text")
    ->get();
```
## 4. Old SQL Query? Just use DB::select()
A pretty typical example is when you have an SQL statement from some older project, and you need to convert it to Eloquent or Query Builder.

Guess what, you don’t have to. DB::select() is a perfectly fine statement.
```php
$results = DB::select('select * from users where id = ?', [1]);
```
## 5. DB::statement() – Usually in Migrations
If you need to execute some SQL query, without processing any results, like INSERT or UPDATE without any parameters, you can use DB::statement().

In my experience, it’s often used in database migrations, when some table structure changes and old data needs to be updated with a new structure.
```php
DB::statement('UPDATE users SET role_id = 1 WHERE role_id IS NULL AND YEAR(created_at) > 2020');
```
Also, `DB::statement()` can perform any SQL query with schema, outside of columns or values.
```php
DB::statement('DROP TABLE users');
DB::statement('ALTER TABLE projects AUTO_INCREMENT=123');
```
**Warning:** be careful with parameters, always validate them