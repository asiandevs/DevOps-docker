## Containerizing PHP Applications

### Step 1: Create a PHP Script

Create a file named `index.php` with the following content:

```php
<?php
    echo "Hello, Docker!";
?>
```

### Step 2: Create a Dockerfile

Create a file named `Dockerfile` (no file extension) in the same directory as your `index.php` with the following content:

```Dockerfile
# Use the official PHP image from the Docker Hub
FROM php:7.4-apache

# Copy the PHP script into the web server's document root
COPY index.php /var/www/html/

# Expose port 80 for the web server
EXPOSE 80
```

This Dockerfile uses the official PHP 7.4 image with Apache from the Docker Hub, copies your `index.php` file to the Apache document root, and exposes port 80.

### Step 3: Build the Docker Image

Open a terminal, navigate to the directory containing your `Dockerfile`, and run the following command to build the Docker image:

```bash
docker build -t mmwebapp .
```

This command builds the Docker image with the tag `my-php-app`. The dot at the end of the command indicates the build context is the current directory.

### Step 4: Run a Docker Container

After successfully building the image, you can run a container from it using the following command:

```bash
docker run -itd --name webapp -p 8080:80 mmwebapp
```

This command maps port 80 inside the container to port 8080 on your host machine. You can choose a different port if needed.

### Step 5: Access the PHP Application

Open your web browser and navigate to `http://<hostpublicIP address>:8080`. You should see the "Hello, Docker!" message from your PHP script.

That's it! You've created a simple PHP Docker image and run a container. 

------------------------------------------------------
Note: I am updating below for testing docker compose [ php (front end] with mysql database]
-------------------------------------------------------
Remember to update the index.php file with your custom PHP script.
```
<html>
<head>
<title>Docker Sample Front App</title>

<?php
if($_SERVER['REQUEST_METHOD'] == "POST")
{
$servername = "dbserver";
$username = "root";
$password = "password";
$dbname = "docker";
$name=$_POST["name"];
$phone=$_POST["phone"];

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);
// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

$sql = "INSERT INTO emp (name, phone)
VALUES ('".$name."', '".$phone."')";

if ($conn->query($sql) === TRUE) {
    echo "New record created successfully";
} else {
    echo "Error: " . $sql . "<br>" . $conn->error;
}

$conn->close();
}
?>
</head>
<body>
        <form action="index.php" method="POST">
                <input type="text" name="name">
                <input type="text" name="phone">
                <input type="submit" name="submit">
        </form>
</body>
</html>
```
