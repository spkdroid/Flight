# Flight

A light weight framework for the PHP

### **1. Prerequisites**
- PHP 7.2 or higher installed
- A web server like Apache or Nginx (you can use PHP's built-in server for simplicity)
- Composer installed for dependency management

---

### **2. Setting Up the Project**

#### Step 1: Create a New Project Directory
```bash
mkdir flight-tutorial
cd flight-tutorial
```

#### Step 2: Initialize Composer
```bash
composer init
```
- Follow the prompts to set up a basic `composer.json` file.

#### Step 3: Install Flight
```bash
composer require mikecao/flight
```

---

### **3. Creating the Project Structure**
Create the following directory structure:

```
flight-tutorial/
├── composer.json
├── index.php
└── views/
    └── home.php
```

---

### **4. Setting Up the Flight Framework**

#### Step 1: Basic Application Setup
Create an `index.php` file:
```php
<?php

require 'vendor/autoload.php';

// Define a route
Flight::route('/', function(){
    echo 'Hello, Flight!';
});

// Start the framework
Flight::start();
```

#### Step 2: Run the Application
Start a built-in PHP server:
```bash
php -S localhost:8000
```
Visit [http://localhost:8000](http://localhost:8000) in your browser. You should see `Hello, Flight!`.

---

### **5. Creating a Simple Web App**

Let’s create a basic web app with routes, a template, and a simple form.

#### Step 1: Add a Template
Create a `views/home.php` file:
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Flight Framework</title>
</head>
<body>
    <h1>Welcome to Flight Framework</h1>
    <form action="/greet" method="POST">
        <input type="text" name="name" placeholder="Enter your name" required>
        <button type="submit">Greet Me</button>
    </form>
</body>
</html>
```

#### Step 2: Serve the Template
Modify `index.php`:
```php
<?php

require 'vendor/autoload.php';

// Route to render the home page
Flight::route('/', function(){
    Flight::render('home');
});

// Route to handle form submission
Flight::route('POST /greet', function(){
    $name = Flight::request()->data->name;
    echo "Hello, " . htmlspecialchars($name) . "!";
});

// Set up the view path
Flight::set('flight.views.path', __DIR__ . '/views');

// Start the framework
Flight::start();
```

#### Step 3: Test the Application
1. Restart the PHP server if it’s running.
2. Visit [http://localhost:8000](http://localhost:8000) to see the form.
3. Submit a name and see the greeting.

---

### **6. Adding JSON Response (Optional)**
Flight makes it easy to work with JSON, making it great for APIs.

Add a new route to `index.php`:
```php
// Route to return JSON response
Flight::route('/api/hello', function(){
    Flight::json(['message' => 'Hello, Flight API!']);
});
```

Visit [http://localhost:8000/api/hello](http://localhost:8000/api/hello) to see a JSON response.

---

### **7. Bonus: Error Handling**
Flight has a simple mechanism for handling errors.

Add an error handler in `index.php`:
```php
Flight::map('notFound', function(){
    echo '404 Not Found!';
});

Flight::map('error', function(Exception $ex){
    echo 'An error occurred: ' . $ex->getMessage();
});
```

---

### **8. Final Code for `index.php`**
```php
<?php

require 'vendor/autoload.php';

// Home route
Flight::route('/', function(){
    Flight::render('home');
});

// Greeting route
Flight::route('POST /greet', function(){
    $name = Flight::request()->data->name;
    echo "Hello, " . htmlspecialchars($name) . "!";
});

// JSON API route
Flight::route('/api/hello', function(){
    Flight::json(['message' => 'Hello, Flight API!']);
});

// Error handling
Flight::map('notFound', function(){
    echo '404 Not Found!';
});

Flight::map('error', function(Exception $ex){
    echo 'An error occurred: ' . $ex->getMessage();
});

// Set views path
Flight::set('flight.views.path', __DIR__ . '/views');

// Start Flight
Flight::start();
```

---

### **9. What’s Next?**
- Add middleware to handle authentication or logging.
- Connect to a database to manage dynamic data.
- Expand your app with more routes and functionality.

This tutorial sets the foundation for building more complex applications with the Flight framework.
