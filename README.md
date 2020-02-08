# Core PHP
- DRY "Don't Repeat Yourself",

## Some Theory
- PHP: Hypertext Preprocessor, Free, Server Side.
- Case insensitive except for variable names.

## echo vs print
- echo is faster than print. print always return true after exec.
- echo "My name is: $name"; accepted but not echo 'My name is: $name'; 

## Constants
```php
// can not be changed
define("GREETING", "Welcome to the world of horrors!");
```

## 'break' and 'continue'
```php
break; // exits from loop,
continue; // go to the next iteration
```

## Super Globals
- Are predefined PHP variables, always accessible.
1. $GLOBALS
- $GLOBALS is a PHP super global variable which is used to access global variables from anywhere in the PHP script.
```php
$x = 75;
$y = 25;
function addition() {
    $GLOBALS['z'] = $GLOBALS['x'] + $GLOBALS['y'];
    // or
    global $z;
}
```

2. $_SERVER
- holds information about headers, paths, and script locations.
- For complete list: [a link](https://www.w3schools.com/php/php_superglobals_server.asp)
```php
echo $_SERVER['PHP_SELF'];
echo $_SERVER['SERVER_NAME'];
echo $_SERVER['HTTP_HOST'];
echo $_SERVER['HTTP_REFERER'];
echo $_SERVER['HTTP_USER_AGENT'];
echo $_SERVER['SCRIPT_NAME'];
```

3. $_REQUEST
- used to collect data after submitting an HTML form.
```php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // collect value of input field
    $name = $_REQUEST['firstName'];
}
```

4. $_POST & $_GET
- used to collect form data
```php
$name = $_POST['fname'];
// or
$name = $_GET['fname'];
```

5. $_FILES
- For PHP file uploading
```php
$target_dir = "uploads/";
$target_file = $target_dir . basename($_FILES["fileToUpload"]["name"]);
- For upload details: [a link](https://www.w3schools.com/php/php_file_upload.asp)
```

6. $_ENV
```php

```

7. $_COOKIE
- A cookie is a small file that the server embeds on the user's computer.
```php
// Create a cookie with setcookie()
setcookie(name, value, expire, path, domain, secure, httponly); 

// Get Cookie
$name = $_COOKIE[$cookie_name];

// modifying a cookie setcookie() same syntax as above

// Delete a cookie
// set the expiration date to one hour ago
setcookie("user", "", time() - 3600);

```
8. $_SESSION
- A session is a way to store information to be used across multiple pages.
- By default, session variables last until the user closes the browser.
```php
// start a PHP session, must be at the top of the page
session_start();
// Set session variables
$_SESSION["favcolor"] = "green";
$_SESSION["favanimal"] = "cat";

// remove all session variables
session_unset();

// destroy the session
session_destroy();
```

## PHP Form Handling:
```php
<!-- action can be the same page: $_SERVER["PHP_SELF"] -->
<form action="handleRequest.php" method="POST"></form>

<!-- Handle form requests -->
if ($_SERVER["REQUEST_METHOD"] == "POST") {}

<!-- prevents Cross-site Scripting attacks in form -->
htmlspecialchars($firstName); 
```

## PHP Date and Time
* Get a Date:
    - d - Represents the day of the month (01 to 31)
    - m - Represents a month (01 to 12)
    - Y - Represents a year (in four digits)
    - l (lowercase 'L') - Represents the day of the week
* Get a Time:
    - H - 24-hour format of an hour (00 to 23)
    - h - 12-hour format of an hour with leading zeros (01 to 12)
    - i - Minutes with leading zeros (00 to 59)
    - s - Seconds with leading zeros (00 to 59)
    - a - Lowercase Ante meridiem and Post meridiem (am or pm)
```php
echo "Today is " . date("Y/m/d"); // use - / : or .
echo "Today is " . date("l");
strtotime(); // Create a date from string
```

## 'include' vs 'require'
- Both used to include files, if file not found 'require' generates a fatal error and stops execution while 'include' does not.

## PHP OOP

- The $this keyword refers to the current object, and is only available inside methods.
- __construct() defines constructor.

### PHP - Access Modifiers
- public - the property or method can be accessed from everywhere. This is default
- protected - the property or method can be accessed within the class and by classes derived from that class
- private - the property or method can ONLY be accessed within the class

### PHP - The final Keyword
- The final keyword can be used to prevent class inheritance or to prevent method overriding.

### PHP - Class Constants
```php
class Goodbye {
    const LEAVING_MESSAGE = "Hello I am constant!!";
    public function byebye() {
        echo self::LEAVING_MESSAGE;
    }
}
echo Goodbye::LEAVING_MESSAGE;
```

### PHP OOP - Abstract Classes and Methiods
- Abstract classes and methods are when the parent class has a named method, but need its child class(es) to fill out the tasks.
- An abstract class is a class that contains at least one abstract method. An abstract method is a method that is declared, but not implemented in the code.
- defined with abstract keyword.
```php
abstract class ParentClass {
  abstract public function someMethod1();
  abstract public function someMethod2($name, $color);
  abstract public function someMethod3() : string;
}

// Parent class
abstract class Car {
  public $name;
  public function __construct($name) {
    $this->name = $name;
  }
  abstract public function intro();
}

// Child classes
class Audi extends Car {
  public function intro(){
    return "Choose German quality! I'm an $this->name!";
  }
}
```

### PHP OOP - Traits
- *PHP only supports single inheritance: a child class can inherit only from one single parent. OOP traits solve this problem.

```php
// syntax
trait TraitName {
  // some code...
}

// In other file
use TraitName;

// Example
trait message1 {
public function msg1() {
    echo "OOP is fun! ";
  }
}
class Welcome {
  use message1;
}
$obj = new Welcome();
$obj->msg1();
```

### PHP OOP - Static Methods
- Static methods can be called directly - without creating an instance of a class.
```php
class Greeting {
  public static function welcome() {
    echo "Hello World!";
  }
  public function insideClassFunc() {
    self::welcome();
  }
}
// Call static method
Greeting::welcome();
```

### PHP - Static Properties (same as above)
- Static properties can be called directly - without creating an instance of a class.
```php
class pi {
  public static $value = 3.14159;
  public function staticValue() {
    return self::$value;
  }
}

// Get static property
echo pi::$value;
```

## PHP with MySQL Database
```php
// connect with DB

$servername = "localhost";
$username = "username";
$password = "password";

// Create connection
$conn = mysqli_connect($servername, $username, $password);

// Check connection
if (!$conn) {
    die("Connection failed: " . mysqli_connect_error());
}
echo "Connected successfully"

// Close connection
mysqli_close($conn);

```

### Running SQL Queries
```php
// Create database
// Create connection
$conn = mysqli_connect($servername, $username, $password);
// Check connection
if (!$conn) {
    die("Connection failed: " . mysqli_connect_error());
}
// Create database
$sql = "CREATE DATABASE myDB";
if (mysqli_query($conn, $sql)) {
    echo "Database created successfully";
} else {
    echo "Error creating database: " . mysqli_error($conn);
}
```