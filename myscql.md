# MySQL

#### Establishing db connection
```php

session_start();

// Database credentials
$dbusername = "root";
$dbpassword = "";
$dbname = "mydb";
$conn = new mysqli("localhost", $dbusername, $dbpassword, $dbname);

// Check the connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
```

#### Mysql connection ending
```php
if ($sql->affected_rows > 0) 
{
    echo "New user has been inserted successfully.";
} 
else 
{
    echo "Failed to insert the user.";
}
$conn->close();

```



#### Check if params are set
```php

// Get requests
if ($_SERVER['REQUEST_METHOD'] === 'GET' && isset($_GET['<url_paramater>']) && ... ) {...} 

// Post Requests
elseif ($_SERVER['REQUEST_METHOD'] === 'POST' && isset($_POST['<post_data_name>']) && ...) { ... } 

// Delete Requests
elseif ($_SERVER['REQUEST_METHOD'] === 'DELETE') {}

```

#### Update Data

```php

$value1 = htmlspecialchars($_POST['<value>']);
$value2 = htmlspecialchars($_POST['<value>']);
$sql = $conn->prepare("UPDATE table SET value1 = ? WHERE value2 = ?");
// "ss" for two strings
$sql->bind_param("ss", $value1, $value2); 
$sql->execute();

```

#### Select Data
```php

// Handling GET request to retrieve user info
$username = htmlspecialchars($_GET['username']);

// Prepare SQL to retrieve user info
$sql = $conn->prepare("SELECT id, username, firstname, lastname FROM users WHERE username = ?");
$sql->bind_param("s", $username); // "s" indicates the parameter is a string
$sql->execute();
$result = $sql->get_result();

if ($result->num_rows > 0) {
    while ($row = $result->fetch_assoc()) {
        echo "User ID: " . $row['id'] . "<br>";
        echo "Username: " . $row['username'] . "<br>";
    }
} else {
    echo "No user found with the username: " . $username;
}
```


#### INSERT data
```php

$username = "john_doe"; // Example data
$firstname = "John";
$lastname = "Doe";

// Prepare the SQL statement
$sql = $conn->prepare("INSERT INTO users (username, firstname, lastname) VALUES (?, ?, ?)");
$sql->bind_param("sss", $username, $firstname, $lastname); // "sss" for three strings
$sql->execute();

if ($sql->affected_rows > 0) {
    echo "New user inserted successfully.";
} else {
    echo "Failed to insert user.";
}

$sql->close();
```



#### Delete
```php
$username = "john_doe"; // Example data

// Prepare the SQL statement
$sql = $conn->prepare("DELETE FROM users WHERE username = ?");
$sql->bind_param("s", $username); // "s" for a single string
$sql->execute();

if ($sql->affected_rows > 0) {
    echo "User deleted successfully.";
} else {
    echo "No user found with that username.";
}

$sql->close();
```


#### Select Sort
```php
<?php
// Prepare the SQL statement to sort by last name
$sql = $conn->prepare("SELECT id, username, firstname, lastname FROM users ORDER BY lastname ASC");
$sql->execute();
$result = $sql->get_result();

if ($result->num_rows > 0) {
    while ($row = $result->fetch_assoc()) {
        echo "ID: " . $row["id"] . " - Name: " . $row["firstname"] . " " . $row["lastname"] . "<br>";
    }
} else {
    echo "No users found.";
}

$sql->close();
?>

```



#### select wild card
```php
<?php
$username = "john"; // Example: search for users starting with "john"

// Prepare the SQL statement with a wildcard
$sql = $conn->prepare("SELECT id, username, firstname, lastname FROM users WHERE username LIKE ?");
$searchTerm = $username . "%"; // Adds the wildcard to the search term
$sql->bind_param("s", $searchTerm); // "s" for string
$sql->execute();
$result = $sql->get_result();

if ($result->num_rows > 0) {
    while ($row = $result->fetch_assoc()) {
        echo "ID: " . $row["id"] . " - Name: " . $row["firstname"] . " " . $row["lastname"] . "<br>";
    }
} else {
    echo "No user found.";
}

$sql->close();
?>

```



#### Select + JSON areturn 
```php
<?php

// Database credentials
$dbusername = "root";
$dbpassword = "";
$dbname = "mydb";

// Create connection
$conn = new mysqli("localhost", $dbusername, $dbpassword, $dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// Prepare the SELECT statement (for example, selecting all users)
$sql = $conn->prepare("SELECT id, username, firstname, lastname FROM users");
$sql->execute();
$result = $sql->get_result();

// Create an array to hold the results
$users = [];

if ($result->num_rows > 0) {
    // Fetch each row and add it to the $users array
    while ($row = $result->fetch_assoc()) {
        $users[] = $row;
    }
}

// Convert the result array to JSON and return it
header('Content-Type: application/json');
echo json_encode($users);

// Close the connection
$conn->close();
?>

```