---
title: The ORM in Action
weight: 2
type: docs
---

**Eloquent Replacing Raw SQL**

The GiftList API uses Eloquent, Laravel's ORM. This means we almost never write SQL directly. Instead, we work with PHP objects that represent database records.

## The Difference

Here's what fetching a gift looks like without an ORM:

```php
// Plain PHP + SQL
$stmt = $pdo->prepare("SELECT * FROM gifts WHERE id = ?");
$stmt->execute([$id]);
$row = $stmt->fetch(PDO::FETCH_ASSOC);

$gift = new Gift();
$gift->id = $row['id'];
$gift->name = $row['name'];
$gift->recipient_id = $row['recipient_id'];
// ... map every field manually
```

And with Eloquent:

```php
// Eloquent
$gift = Gift::find($id);
```

One line. The ORM handles the query, the mapping, and the object creation.

## Relationships

Eloquent shines with relationships. In GiftList, a Recipient has many Gifts:

```php
// In Recipient model
public function gifts()
{
    return $this->hasMany(Gift::class);
}

// Usage
$recipient = Recipient::find($id);
$gifts = $recipient->gifts;  // All gifts for this recipient
```

No join queries. No manual mapping. Declare the relationship once; use it everywhere.

## Automatic Protection

Every Eloquent query uses parameterized statements. SQL injection is prevented by default:

```php
// This is safe—Eloquent escapes the input
$gifts = Gift::where('name', $userInput)->get();
```

You'd have to go out of your way to create a vulnerability.

## The 90% Reduction

ORMs can reduce database code by 90% or more. Compare a typical CRUD operation:

**Without ORM:** Query building, execution, error handling, result fetching, object mapping, relationship loading—easily 50+ lines per operation.

**With Eloquent:** Model definition plus one-liners for each operation—maybe 10 lines total.

The ORM eliminates boilerplate so you can focus on business logic.

## When to Drop Down

Eloquent isn't magic. Complex reports, bulk operations, or performance-critical queries sometimes need raw SQL:

```php
$results = DB::select('SELECT ... complex query ...');
```

Good ORMs make this easy. Use the abstraction when it helps; escape it when you need to.
