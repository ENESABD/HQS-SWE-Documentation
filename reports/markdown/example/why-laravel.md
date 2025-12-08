---
title: Why Laravel?
weight: 1
type: docs
---

**How the Framework Solves Common Problems**

The GiftList API could have been built in plain PHP. It would work. But it would also require writing authentication from scratch, manually handling database connections, building a routing system, sanitizing inputs, and dozens of other tasks that have nothing to do with gift tracking.

Laravel handles all of that. Here's what it gives us:

## High-Level Abstraction

Laravel abstracts away the plumbing. Instead of configuring PDO connections and writing query builders, you describe what you want:

```php
// Get all gifts for a recipient
$gifts = Gift::where('recipient_id', $id)->get();
```

The framework handles connections, prepared statements, result mapping, and error handling.

## Built-in Security

Security is hard to get right. Laravel provides:

- **CSRF protection** — Automatic on all forms
- **SQL injection prevention** — Eloquent uses parameterized queries
- **Authentication scaffolding** — Sanctum handles API tokens
- **Middleware** — Apply security checks declaratively

In the GiftList API, protecting a route is one line:

```php
Route::middleware('auth:sanctum')->group(function () {
    // These routes require authentication
});
```

## MVC Structure

Laravel enforces Model-View-Controller separation:

- **Models** define data and relationships (`Gift.php`, `Recipient.php`)
- **Controllers** handle HTTP requests and responses
- **Routes** map URLs to controller methods

This structure means any Laravel developer can navigate the codebase immediately. No guessing where things live.

## REST API Made Simple

Building a REST API in plain PHP means manually parsing requests, formatting JSON responses, handling HTTP status codes, and managing content types. Laravel's resource controllers and API resources handle it all:

```php
// One line to define all CRUD routes
Route::apiResource('gifts', GiftController::class);
```

This generates `GET /gifts`, `POST /gifts`, `GET /gifts/{id}`, `PUT /gifts/{id}`, and `DELETE /gifts/{id}`—all properly routed to controller methods.

## The Trade-Off

Laravel is opinionated. You work within its conventions. For GiftList, that's perfect—we don't need custom routing or exotic database patterns. The conventions accelerate development.

For projects with unusual requirements, those same conventions might become constraints. Choose frameworks whose opinions match your problem.
