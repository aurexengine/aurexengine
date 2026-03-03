# AurexEngine

> A modular PHP framework builder designed for flexibility, scalability,
> and long-term ecosystem growth.

AurexEngine is not just a framework.

It is a **framework ecosystem** built to allow developers to:

-   Build web applications
-   Create their own framework distributions
-   Compose modular packages
-   Control updates without version conflicts
-   Ship lightweight or full-stack setups

------------------------------------------------------------------------

## 🚀 Installation

create a starter application:

``` bash
composer create-project aurexengine/skeleton my-app
```

------------------------------------------------------------------------

## 📦 What is `AurexEngine`?

This package acts as the **entry point and meta distribution** of the
Aurex ecosystem.

It pulls together the official core components:

-   `aurexengine/core`
-   `aurexengine/http`
-   `aurexengine/routing`
-   `aurexengine/mvc`
-   `aurexengine/database`
-   `aurexengine/auth`

Think of it as:

> The full AurexEngine stack --- modular but unified.

------------------------------------------------------------------------

## 🧱 Architecture Philosophy

AurexEngine is built around modular separation:

### Core

Container, application lifecycle, service providers, configuration,
environment loading.

### HTTP

Request, response, middleware pipeline, kernel.

### Routing

Router, route groups, parameters, dispatching.

### MVC

Controller base class and view rendering.

### Database

PDO connection manager, query builder, migrations.

### Auth

Session-based authentication system.

Each package can be used independently.

------------------------------------------------------------------------

## 🎯 Why AurexEngine?

### 1️⃣ Modular by Design

You can require only what you need:

``` bash
composer require aurexengine/core
```

or

``` bash
composer require aurexengine/database
```

Or install the full stack.

------------------------------------------------------------------------

### 2️⃣ Framework Builder Concept

AurexEngine allows you to:

-   Build your own framework distribution
-   Create custom skeletons
-   Publish reusable modules
-   Compose your own architecture

------------------------------------------------------------------------

### 3️⃣ Clean Upgrade Path

Because the ecosystem is modular:

-   You can update specific packages
-   You avoid massive framework conflicts
-   You maintain control over versions

------------------------------------------------------------------------

### 4️⃣ Lightweight Yet Expandable

Start minimal. Scale when needed.

------------------------------------------------------------------------

## 🛠 Example Usage

``` php
$router->get('/', function () {
    return 'Hello AurexEngine';
});
```

Controller example:

``` php
class HomeController extends Controller
{
    public function index()
    {
        return $this->view('home.index');
    }
}
```

Query example:

``` php
$users = db()->table('users')->whereEq('id', 1)->first();
```

Authentication:

``` php
auth()->attempt([
    'email' => 'user@example.com',
    'password' => 'secret'
]);
```

------------------------------------------------------------------------

## 🏗 Ecosystem Packages

  Package                Description
  ---------------------- --------------------------
  aurexengine/core       Foundation & container
  aurexengine/http       HTTP kernel & middleware
  aurexengine/routing    Routing system
  aurexengine/mvc        MVC layer
  aurexengine/database   Database & migrations
  aurexengine/auth       Authentication

------------------------------------------------------------------------

## 🧭 Roadmap

-   Console / CLI (`aurex` command)
-   Reactive components (Wire-like system)
-   Policy & Authorization
-   Queue system
-   Caching layer
-   Package publishing system
-   Desktop runtime support

------------------------------------------------------------------------

## 📖 Vision

AurexEngine aims to be:

> A modern PHP engine where developers can build their own framework
> flavor instead of being locked into one.

It is inspired by modern ecosystems but designed for flexibility and
control.

------------------------------------------------------------------------

## 🤝 Contributing

Contributions are welcome.

Open issues or pull requests in the respective package repository.

------------------------------------------------------------------------

## 📜 License

MIT
