# javascaript


#### GEt, POST, UPDATYE, and DELETE
```js
// Function to initialize any necessary components (if needed)
function initialize() {
    console.log("Initialization complete.");
}

// GET Request: Fetch data from the server
function getData() {
    var ajax = new XMLHttpRequest();
    var searchTermValue = document.getElementById('search_phrase').value;
    var queryString = "process.php?phrase=" + encodeURIComponent(searchTermValue);

    ajax.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            console.log('GET request sent successfully!');
            console.log(`Response = ${this.response}`);
        }
    };

    // Open the GET request
    ajax.open("GET", queryString, true);

    // Send the GET request (no body needed for GET)
    ajax.send(null);
}


// POST Request: Insert data into the server (e.g., adding a new record)
function postData() {
    var ajax = new XMLHttpRequest();
    var username = document.getElementById('post_data').value;
    var url = "process.php";

    // Create the POST data (URL-encoded)
    var postData = "username=" + encodeURIComponent(username);

    ajax.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            console.log('POST request sent successfully!');
            console.log(`Response = ${this.response}`);
        }
    };

    // Open the POST request
    ajax.open("POST", url, true);

    // Set the content type to application/x-www-form-urlencoded
    ajax.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");

    // Send the POST data in the body
    ajax.send(postData);
}


// PUT/UPDATE Request: Update existing data on the server
function updateUser() {
    var ajax = new XMLHttpRequest();
    var username = document.getElementById('username').value;
    var newFirstName = document.getElementById('new_firstname').value;
    var url = "process.php";

    // Prepare the data to be sent (URL-encoded)
    var updateData = "username=" + encodeURIComponent(username) + "&firstname=" + encodeURIComponent(newFirstName);

    ajax.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            console.log('PUT/UPDATE request sent successfully!');
            console.log(`Response = ${this.response}`);
        }
    };

    // Open the PUT/UPDATE request (note: we use POST in PHP as it doesn't natively support PUT)
    ajax.open("POST", url, true);

    // Set the content type to application/x-www-form-urlencoded
    ajax.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");

    // Send the update data in the body
    ajax.send(updateData);
}


// DELETE Request: Remove data from the server
function deleteUser() {
    var ajax = new XMLHttpRequest();
    var username = document.getElementById('username').value;

    // Prepare the DELETE request with the data in the query string
    var url = "process.php?username=" + encodeURIComponent(username);

    ajax.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            console.log('DELETE request sent successfully!');
            console.log(`Response = ${this.response}`);
        }
    };

    // Open the DELETE request
    ajax.open("DELETE", url, true);

    // Send the DELETE request (usually no body is needed for DELETE)
    ajax.send(null);
}

```