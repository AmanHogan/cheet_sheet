### PHP
#### Concatenation
```php
<?php
$name = "Aman";
echo "Name  is " . $name . "<br>";
echo "Name  is $name.";
echo "<h2>PHP is Fun!</h2>";
echo "This ", "string ", "multiple parameters.";
?>
```

`var_dump($x)` - returns data type and size, ex `var_dump("Hi") :: string(2)`

#### Strings

#### Concatenate
```php
$x = "Hello";
$y = "World";
$z = $x . $y;
echo $z;
```

#### Replace string
```php
$x = "Hello World!";
echo str_replace("World", "Dolly", $x);
```


#### Remove whitespace
```php
$x = " Hello World! ";
echo trim($x);
```
#### Str to array
```php
$x = "Hello World!";
$y = explode(" ", $x);

//Use the print_r() function to display the result:
print_r($y);

/*
Result:
Array ( [0] => Hello [1] => World! )
*/
```

#### Slicing Strings
```php
$x = "Hello World!";
echo substr($x, 6, 5);
```
---


#### For loop
```php
for ($x = 0; $x <= 10; $x++) {
  echo "The number is: $x <br>";
}

for ($x = 0; $x <= 10; $x++) {
  if ($x == 3) continue;
  echo "The number is: $x <br>";
}

```


#### Foreach loop
```php
$colors = array("red", "green", "blue", "yellow");
// For every loop iteration, the value of the current 
// array element is assigned to the variabe 
//$x. The iteration continues until
// it reaches the last array element.
foreach ($colors as $x) {
  echo "$x <br>";
}


// Can do the same with key and values
$members = array("Peter"=>"35", "Ben"=>"37", "Joe"=>"43");

foreach ($members as $x => $y) {
  echo "$x : $y <br>";
}


// Either syntax is acceptable
$y = [
    "val" => 1
];

$y = array("val" => 1);
```

#### For each by ref
```php
/*
Oringal changes are made to array, now that its done by refernce. Vefoire it wasnt changed.
*/
$colors = array("red", "green", "blue", "yellow");

foreach ($colors as &$x) {
  if ($x == "blue") $x = "pink";
}

var_dump($colors);

```

---

#### Function syntax

```php
function familyName($fname, $year) {
  echo "$fname Refsnes. Born in $year <br>";
}

familyName("Hege", "1975");

// returning a value
function sum($x, $y) {
  $z = $x + $y;
  return $z;
}

echo "5 + 10 = " . sum(5, 10) . "<br>";


// pass by refernce
function add_five(&$value) {
  $value += 5;
}

$num = 2;
add_five($num);
echo $num;

```


#### function, variable args
```php

// variadic variable is last
function myFamily($lastname, ...$firstname) {
  txt = "";
  $len = count($firstname);
  for($i = 0; $i < $len; $i++) {
    $txt = $txt."Hi, $firstname[$i] $lastname.<br>";
  }
  return $txt;
}

$a = myFamily("Doe", "Jane", "John", "Joey");
echo $a;

```


#### Updating arrays

```php

$cars = array("Volvo", "BMW", "Toyota");
$cars[1] = "Ford";

$cars = array("brand" => "Ford", "model" => "Mustang", "year" => 1964);
$cars["year"] = 2024;

// Update each item in array. 
// must unset x so that last item
$cars = array("Volvo", "BMW", "Toyota");
foreach ($cars as &$x) {
  $x = "Ford";
}
unset($x);
var_dump($cars);
```


#### Adding array items

```php

$fruits = array("Apple", "Banana", "Cherry");
$fruits[] = "Orange";

$cars = array("brand" => "Ford", "model" => "Mustang");
$cars["color"] = "Red";

// adds three items
$fruits = array("Apple", "Banana", "Cherry");
array_push($fruits, "Orange", "Kiwi", "Lemon");

// adds multiple items
$cars = array("brand" => "Ford", "model" => "Mustang");
$cars += ["color" => "red", "year" => 1964];

```


#### Removing array items

```php

$cars = array("Volvo", "BMW", "Toyota");
unset($cars[1]);

$cars = array("Volvo", "BMW", "Toyota");
array_splice($cars, 1, 2);


$cars = array("Volvo", "BMW", "Toyota");
unset($cars[0], $cars[1]);

$cars = array("brand" => "Ford", "model" => "Mustang", "year" => 1964);
unset($cars["model"]);


```

#### Sorting an array
```php
// alphabetticall
$cars = array("Volvo", "BMW", "Toyota");
sort($cars);

// numerical
$numbers = array(4, 6, 2, 22, 11);
sort($numbers);

// sort ascending based on value
$age = array("Peter"=>"35", "Ben"=>"37", "Joe"=>"43");
asort($age);

// sort assending based on key
$age = array("Peter"=>"35", "Ben"=>"37", "Joe"=>"43");
ksort($age);
```


#### Super GLobals
In other words, $_REQUEST is an array containing data from $_GET, $_POST, and $_COOKIE.
```html
<html>
<body>

<form method="post" action="<?php echo $_SERVER['PHP_SELF'];?>">
  Name: <input type="text" name="fname">
  <input type="submit">
</form>

<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
  $name = htmlspecialchars($_REQUEST['fname']);
  if (empty($name)) {
    echo "Name is empty";
  } else {
    echo $name;
  }
}
?>

</body>
</html>


```


#### Ways to fetch data from php


### Two Approaches to Handling a GET Request:

1. **Using a Simple HTML Form with PHP:**
   - When you submit a form using the standard `GET` or `POST` method, the page reloads, and the data is sent to the server.
   - This triggers the PHP script to handle the request, and the browser will load a new page (or the same page) with the server’s response.
   
   **Example of a Basic HTML Form (GET request):**
   ```html
   <form action="process.php" method="GET">
       <input type="text" name="query" placeholder="Enter your search">
       <input type="submit" value="Submit">
   </form>
   ```

   - When the user submits the form, the browser navigates to `process.php` and appends the form data as a query string (e.g., `process.php?query=value`).
   - The browser **reloads** the page to show the response from the server.

2. **Using JavaScript to Make an AJAX GET Request to PHP (Without Page Reload):**
   - Instead of submitting the form directly and causing a page reload, you can handle the form submission with JavaScript (specifically, using **AJAX**).
   - This allows you to make a **GET request** to a PHP script and retrieve data from the server **without refreshing the page**.

   **Example: Using JavaScript to Send a GET Request to PHP:**
   
   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>AJAX GET Request Example</title>
       <script>
           function fetchData() {
               // Get the input value
               var query = document.getElementById('queryInput').value;
               
               // Create a new XMLHttpRequest object
               var xhr = new XMLHttpRequest();
               
               // Define what happens when the request is successful
               xhr.onreadystatechange = function() {
                   if (xhr.readyState === 4 && xhr.status === 200) {
                       // Update the content of the result div with the response from PHP
                       document.getElementById('result').innerHTML = xhr.responseText;
                   }
               };
               
               // Open a GET request to the PHP script
               xhr.open('GET', 'process.php?query=' + encodeURIComponent(query), true);
               
               // Send the GET request
               xhr.send();
           }
       </script>
   </head>
   <body>
       <form onsubmit="event.preventDefault(); fetchData();">
           <input type="text" id="queryInput" placeholder="Enter your search">
           <input type="button" value="Submit" onclick="fetchData()">
       </form>

       <!-- Div to display the result -->
       <div id="result"></div>
   </body>
   </html>
   ```

   - **Explanation:**
     - The `onsubmit="event.preventDefault(); fetchData();"` prevents the form from submitting normally and reloading the page.
     - `fetchData()` is a JavaScript function that creates an `XMLHttpRequest` object to send a **GET request** to the `process.php` script.
     - The query string is dynamically appended to the URL (`process.php?query=yourValue`), just like it would be in a form submission.
     - The server response is handled within the `onreadystatechange` function, where the response (from the PHP script) is displayed in the `<div id="result"></div>` element.

### Example of PHP (`process.php`) to Handle the AJAX GET Request:

```php
<?php
// Check if the 'query' parameter is set in the GET request
if (isset($_GET['query'])) {
    $query = htmlspecialchars($_GET['query']);  // Sanitize the input for security
    
    // Perform some operation based on the query (e.g., search a database, etc.)
    echo "You searched for: " . $query;
} else {
    echo "No query parameter provided.";
}
?>
```

### Key Differences Between These Approaches:

- **HTML Form Submission (Normal GET Request):**
  - Causes a full page reload.
  - Data is sent to the server via the URL query string (with `method="GET"`).
  - The browser navigates to a new page (or the same page) to display the server's response.

- **JavaScript AJAX Request (GET Request Using JavaScript):**
  - Does **not reload** the page.
  - Allows you to send a GET request to the server and dynamically retrieve information without leaving the current page.
  - The server's response can be updated in a specific section of the page (using `innerHTML`, for example).
  - Provides a more interactive, seamless user experience.

### Summary:

- If you submit a form with a normal HTML form submission, the browser will **reload** the page.
- If you use **JavaScript (AJAX)** to send a GET request to the PHP script, you can retrieve data from the server **without reloading the page**. This is useful for building interactive web applications.

Both methods work with PHP, but AJAX is more flexible and provides a smoother user experience when you want to dynamically update content without a full page reload.

---

#### Sessions


Should start a session at your index php:It’s best practice to **start the session at the very beginning** of your application, such as in your `index.php` or any other initial script that the user first visits. This ensures that session data is available throughout the user’s interaction with your website, no matter which page or PHP script they access.

### Here's why you should start the session in `index.php`:

1. **Consistency**: Starting the session at the very beginning (such as in `index.php`) ensures that session data is initialized and available for any subsequent PHP script, even if those scripts don’t directly handle session data.
2. **Access Across the Application**: Once a session is started, session variables can be accessed or modified from any PHP script, so initializing it early ensures the session is ready throughout the entire application.
3. **Prevents "Headers Already Sent" Errors**: If you wait until later in the application (like in a backend script), and output (HTML, headers, etc.) is already sent to the browser, trying to start a session later may result in errors. This happens because PHP sessions send headers to the browser, which must be done before any output is sent.

### Best Practice: Start Session at the Beginning

- **`index.php`** is often the entry point for most web applications, and it’s a common place to initialize things like sessions, configuration settings, and database connections.
- You should call `session_start()` at the top of your main PHP entry point file (`index.php` or similar), ensuring the session starts before any output is sent to the browser.

### Example: Starting a Session in `index.php`

```php
<?php
session_start();  // Start the session as soon as the user accesses the site
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My PHP Application</title>
</head>
<body>
    <h1>Welcome to My Application</h1>
    <?php
    // Initialize session variables if needed
    if (!isset($_SESSION['username'])) {
        $_SESSION['username'] = 'Guest';  // Default value
    }

    echo "Hello, " . $_SESSION['username'];
    ?>
</body>
</html>
```

### What if Multiple PHP Scripts Are Called?

If you have multiple PHP scripts (e.g., `backend.php`, `process.php`, etc.), you will need to start the session on every page where you want to access or modify session variables. **Every PHP script that interacts with session data must have `session_start()`** at the beginning of the script.

### Example: A Backend Script

For example, if `process.php` or any other PHP script is accessed via an AJAX request or a form submission and it needs to access session data, it also needs `session_start()`:

```php
<?php
session_start();  // Start the session in every script where you want to access session data

// Check or modify session variables
if (isset($_SESSION['username'])) {
    echo "Hello, " . $_SESSION['username'];
} else {
    echo "Session not set!";
}
?>
```

### Summary:
- **Start the session in `index.php` or any initial script** that the user first reaches. This ensures session handling is initialized early in the application.
- **Include `session_start()` at the top of any other PHP script** that interacts with session variables.
- This ensures that session variables are available across all pages without encountering "headers already sent" errors or losing session data.



#### Response and REponseTExt

```js
var xhr = new XMLHttpRequest();
xhr.open('GET', 'process.php', true);
xhr.responseType = 'json';  // Set responseType to 'json'

xhr.onload = function() {
    if (xhr.status == 200) {
        console.log(xhr.response);  // No need to parse, already a JS object
    }
};

xhr.send();
```

Example: When to Use responseText

javascript

```js
var xhr = new XMLHttpRequest();
xhr.open('GET', 'process.php', true);

xhr.onload = function() {
    if (xhr.status == 200) {
        console.log(xhr.responseText);  // Raw JSON string
        var data = JSON.parse(xhr.responseText);  // Manually parse the JSON
        console.log(data);
    }
};

xhr.send();
```