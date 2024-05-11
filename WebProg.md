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
