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


### Close Connection

- Don't forget, when you've finished playing with your database to make sure that you close the connection:

```php
$db->close();
```

### Final Conclusion
- Using ```mysql_``` functions is a foolish move to make.
- *Don't use these outdated and useless methods* because they're easier, or quicker.
- Man up and tackle the new forms of database interaction - ```MySQLi```.
  - You'll make better and secure code



## 2. Bootstrap

https://webtechnologies.site/files/b05/final/presentations/bootstrap-170319142352.pdf

## 3. PHP to sql

https://webtechnologies.site/files/b05/final/presentations/phpTOsql.pdf

## 4. HTML Form

### HTML forms
- An HTML form is used to collect user input. 
- The user input is most often sent to a server for processing.

### The ```<form>``` element
- The HTML ```<form>``` element is used to create an HTML form for user input:

```html
<form>
    .
    form elements
    .
</form>
```

### The ```<input>``` element
- The HTML ```<input>``` element is the most used form element.
- An ```<input>``` element can be displayed in many ways, depending on the type attribute.
- Example
![alt text](image.png)


### The ```action``` attribute
- The action attribute defines the action to be performed when the form is submitted. 
- Usually, the form data is sent to a file on the server when the user clicks on the submit button.

```html
<form action="/action_page.php">
    <label for="fname">First name:</label><br>
    <input type="text" id="fname" name="fname" value="John"><br>
    <label for="lname">Last name:</label><br>
    <input type="text" id="lname" name="lname" value="Doe"><br><br>
    <input type="submit" value="Submit">
</form>
```


### The ```method``` attribute
- The method attribute specifies the HTTP method tobe used when submitting the form data.
- The form-data can be sent as URL variables (with ```method="get"```) or as HTTP post transaction (with ```method="post"```).

```html
<form action="/action_page.php" method="get">
```
or
```html
<form action="/action_page.php" method="post">
```

**Notes on GET:**
- Appends the form data to the URL, in name/value pairs
- *NEVER use GET to send sensitive data!* (the submitted form data is
visible in the URL!)
- The length of a URL is limited (2048 characters)
- Useful for form submissions where a user wants to bookmark the result
- GET is good for non-secure data, like query strings in Google

**Notes on POST:**
- Appends the form data inside the body of the HTTP request (the
submitted form data is not shown in the URL)
- POST has no size limitations, and can be used to send large amounts of data.
- Form submissions with POST cannot be bookmarked


# Web Prog Midterms

## 1. MySQL
https://docs.google.com/document/d/1LY5oa3IKzZyuZhi-XRto0B7FDAjzvUm_RTrNoJu2iBE/edit?usp=sharing


### MySQL
Its name is a combination of:
- **"My"**, 
  - the name of co-founder Michael Widenius's daughter My, 
- **"SQL"**, 
  - the acronym for ```Structured Query Language```.
  - It is a very popular open-source relational database management system
### SQL ( Structured Query Language)
- Is used to ```insert```, ```search```, ```update```, and ```delete``` database records

- **CRUD OPERATIONS**
  - ```SELECT``` - extracts data from a database
  - ```UPDATE``` - updates data in a database
  - ```DELETE``` - deletes data from a database
  - ```INSERT INTO``` - inserts new data into a database
- **DATABASE FUNCTIONS**
  - ```CREATE DATABASE``` - creates a new database
  - ```ALTER DATABASE``` - modifies a database
- **TABLE FUNCTIONS**
  - ```CREATE TABLE``` - creates a new table
  - ```ALTER TABLE``` - modifies a table
  - ```DROP TABLE``` - deletes a table
- **INDEXING**
  - ```CREATE INDEX``` - creates an index (search key)
  - ```DROP INDEX``` - deletes an index

### SQL CRUD (Create, Read, Update, Delete)
**1. CREATE**

- ```INSERT INTO``` statement
  - Used to insert new records in a table
  
Syntax:
``` sql
    INSERT INTO table_name (column1, column2, column3, ...)
    VALUES (value1, value2, value3, ...);
```

``` sql
    INSERT INTO table_name
    VALUES (value1, value2, value3, ...);
```
Ex:
```sql
    INSERT INTO Customers (CustomerName, ContactName,
    Address, City, PostalCode, Country)
    VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen
    21', 'Stavanger', '4006', 'Norway');
```
**2. READ**
- ```SELECT``` statement
  - Used to select data from a database

Syntax:
```sql
SELECT * FROM table_name;
// The “*” means all
// This statement basically means select all data // from the table
```

```sql
SELECT column1, column2, ...
FROM table_name;
// This statement means select these specific 
// column from the table
```
Example:
```sql
SELECT CustomerName, City, Country 
FROM Customers;
```

- ```WHERE``` Clause
  - A conditional statement
  - Used to filter data based on condition/s
  
Syntax:
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```
EX:
```sql
SELECT * FROM Customers
WHERE Country = 'Mexico';
```

- ```AND```, ```OR``` and ```NOT``` Operators
  - Creating a query with only one condition is not sufficient. 
  - Sometimes we would like to check something more complicated. For that SQL (and many other programming languages) have the ```AND```, ```OR```, and ```NOT``` keywords to increase our ability to fetch the right result we need.

The AND, OR, and NOT keywords are used like this:
```sql
SELECT col1, col2 
FROM table1
WHERE NOT condition1 AND condition2 OR condition3 ...
// We can stack as many conditions as we want together.

```
- ```ORDER BY``` keyword
- Used to sort the selected data using the selected column itself or another column or by condition  in ```desc``` or ```asc```.
  
Syntax:
```sql
SELECT *
FROM table_name
WHERE condition
ORDER BY columnName/condition DESC/ASC
// by default, it sorts in ascending order.
```
For example

```sql
SELECT *
FROM competition
WHERE age > 50
ORDER BY avg_speed
```

**3. UPDATE**
- ```UPDATE``` statement 
  - is used to modify the existing records in a table
  - It uses the ```SET``` keyword to modify data

Syntax: 
```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```
EX:
```sql
UPDATE Customers
SET ContactName = 'Alfred Schmidt', City = 'Frankfurt'
WHERE CustomerID = 1;
```

**4. DELETE**
- ```DELETE``` statement
  - used to delete existing records in a table.

Syntax:
```sql
DELETE FROM table_name;
DELETE FROM table_name WHERE condition;
```
EX:
```sql
DELETE FROM Customers 
WHERE CustomerName='Alfreds Futterkiste';
```
## 2. Javascript
https://webtechnologies.site/javascript.pdf

### ABOUT JAVASCRIPT
- JAVASCRIPT IS A **PROGRAMMING LANGUAGE.**
- JAVASCRIPT IS *OBJECT BASED PROGRAMMING LANGUAGE* NOT OBJECT ORIENTED.
- JAVASCRIPT AND JAVA ARE NOT SAME.
- JAVASCRIPT IS WEAKLY TYPED, **CLIENT SIDE** INTERPRETED LANGUAGE.
- DESIGNED BY BRENDAN EICH FOR NETSCAPE.
- IT WAS ORIGINALLY CALLED ```MOCHA```, RENAMED TO ```LIVESCRIPT```, AND THEN RENAMED TO ```JAVASCRIPT```. 
- THE OFFICIAL STANDARD IS JUST CALLED **```ECMASCRIPT```**

### Internal and External usage of JS in HTML

- **Internal**
  - use the ```<script>``` tag to use javascript in HTML
  - It is internal because the ```<script>``` with js code is within the HTML document 
```html
<script>
  document.getElementById("demo").innerHTML = "My First JavaScript";
</script>
```

- **External**
  - use also the ```script``` tag to externall add JS file in the html
  - add the js file as the value for the ```src``` attribute
```html
<script src="myScript.js"></script>
```

### Display
- ```console.log()``` statement
  - It is used in javascript to display something (terminal)

```js
console.log("Hello, World!");
```

### Comments

- Comments are used to add text in your code that isn't read by the compiler

**Types of Comments used in JS**
- ``//`` single-line comment

```js
// This is ghost of caritan
```
- ``/* */`` multi-line comment
```js
/*
Ghost 
of 
Caritan
*/
```


### Function
- Functions are a block of code that can be reusable within your code
- Designed to perform a particular task.
- The ```function``` keyword is used to create functions in javascript followed by the function name and parenthesis (with or without arguments)


Syntax:
```js
function myFunction() {
    // Your code here
}
```
- To invoke the function, just call the function followed by its argument

```js
myFunction();
```

Example:
```js
// Function to compute the product of p1 and p2
function myFunction(p1, p2) {
  return p1 * p2;
}
```
 

## 3. PHP (PHP: Hypertext Preprocessor)
https://webtechnologies.site/PHP.pdf
### About PHP
- It is a open-source Scripting language
- Can contain ```text```, ```html```, ```js```, and ``php`` code
- PHP code is executed on a server, and the result is retuned to the browser as a plain html

### PHP basic syntax

- A PHP SCRIPT CAN BE PLACED ANYWHERE IN THE DOCUMENT.
- A PHP SCRIPT STARTS WITH ```<?PHP``` AND ENDS WITH ```?>```

Syntax:
```php
<?PHP
// PHP CODE GOES HERE
?>
```

### Display
- ```echo``` statement
  - It is used to display something in php

Example:
```php
<?php
  echo "Hello, World!";
?>
```

**Note:** Php statements ends with semicolon ```;``` 

### Variables
- Variables in PHP are **case-sensitive**
- Every variable in php must starts with the dollar sign ```$```

Syntax:
```php
<?php
  $myVariable = "red";
  $MyVariable = "blue";

  // Note the two declared and initialized variable are different variables 
  // $myVariable != $MyVariable

?>

```

### Comments 
- Comments are used to add text in your code that isn't read by the compiler

**Types of Comments used in PHP**
- ```//``` Single-line comment

```php
<?php
// Ghost of Caritan
?> 
```

- ```#``` also a single-line comment
```php
<?php
# Ghost of Caritan
?>
```

- ```/* */``` multi-line comment
```php
<?php
/* 
  Ghost 
  of 
  Caritan
*/
?>
```

### Concatenation 
- in PHP, the dot ```.``` sign is used to concatenate 

Example:
```php
<?php
    $myVariable = "Caritan";
    echo "Ghost of " . $myVariable;

  // Output: Ghost of Caritan
?>
```


## 4. CSS Responsive
https://webtechnologies.site/css-responsive.pdf
