# Web Prog Finals

## 1. MySQLi

### Setup Connection
- Instantiating new instance of MySQLi
```php 
$db = new mysqli('localhost', 'ROOT_USERNAME’,'ROOT_PASSWORD', 'DATABASE');
if($db->connect_errno > 0){
    die('Unable to connect to database [' . $db->connect_error .']');
}
```

### Query
- Example: pull out all of the users from the users table where they have status = ‘active’.

```php
$sql = "SELECT * FROM `users` WHERE `status` = 'active' ";
if(!$result = $db->query($sql)){
    die('There was an error running the query [' . $db->error . ']');
}
```

### Output Query Results
- To loop through the results and output the username for each row on a new line
  - Example:
    ```php
    while($row = $result->fetch_assoc()){
        echo $row['username'] . '<br />';
    }
    ```
    or 
    ```php
    while($row = $result->fetch_object()){
        echo $row->username . '<br />';
    }
    ```

### Number of returned rows
- Each mysqli_result object that is returned has a variable defined which is called ```$num_rows```, so all we need to do is access that variable by doing:

```php
<?php
    echo 'Total results: ' . $result->num_rows;
?>
```

### Number of affected rows
- When running an ```UPDATE``` query you sometimes want to know how many rows have been updated, or deleted if running a ```DELETE``` query, this is a variable which is inside the mysqli object.
  - Example:
```php
<?php
    echo 'Total rows updated: ' . $db->affected_rows;
?>
```

### Free result

- It's advisable to free a result when you've finished playing with the result set, so in the above example we should put the following code after our ```while()``` loop:
  - Example:
```php
    $result->free();
```
- This will free up some system resources, and is a good practice to get in the habit of doing.

### Escaping Characters
- When inserting data into a database, we'll have been to escape it first, so that single quotes get preceded by a backslash.
```php
$db->real_escape_string('This is an unescaped "string"');
```
- However, because this is a commonly used function, there is an alias function that you can use which is shorter andless to type:
```php
$db->escape_string('This is an unescape "string"');
```
- This string should now be safer to insert into your database through a query.


## Close Connection

- Don't forget, when you've finished playing with your database to make sure that you close the connection:

```php
$db->close();
```



