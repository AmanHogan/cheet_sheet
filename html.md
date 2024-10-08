### HTML

#### New page, get
```html
<!-- Form with GET method -->
    <form action="process.php" method="GET">
        <label for="username">Username:</label>
        <input type="text" id="username" name="username" placeholder="Enter your username" required><br>
        
        <label for="age">Age:</label>
        <input type="number" id="age" name="age" placeholder="Enter your age" required><br>

        <!-- Submit button -->
        <input type="submit" value="Submit">
    </form>
    <!--process.php?username=john&age=30 
    $username = $_GET['username'];
    $age = $_GET['age'];
    -->
```


#### New page, post
```html
 <!-- Form with POST method -->
    <form action="process.php" method="POST">
        <label for="username">Username:</label>
        <input type="text" id="username" name="username" placeholder="Enter your username" required><br>
        
        <label for="age">Age:</label>
        <input type="number" id="age" name="age" placeholder="Enter your age" required><br>

        <!-- Submit button -->
        <input type="submit" value="Submit">
    </form>

    <!-- $username = $_POST['username'];
$age = $_POST['age']; -->
```


#### Proccessing forms in php for new pages
```php
<?php
// Check the request method
if ($_SERVER['REQUEST_METHOD'] === 'GET') {
    // Handle GET request
    $username = $_GET['username'];
    $age = $_GET['age'];
    echo "GET request received.<br>";
    echo "Username: $username<br>";
    echo "Age: $age<br>";
} elseif ($_SERVER['REQUEST_METHOD'] === 'POST') {
    // Handle POST request
    $username = $_POST['username'];
    $age = $_POST['age'];
    echo "POST request received.<br>";
    echo "Username: $username<br>";
    echo "Age: $age<br>";
} else {
    echo "Invalid request method.";
}
?>
```