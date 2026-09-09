---
title: Database Performance & Eloquent N+1 Optimization
tags:
  - php
  - laravel
  - eloquent
  - database
  - sql
  - optimization
related_notes:
  - "[[Senior PHP Bug Solving & Architecture Blueprint]]"
  - "[[Memory Leak Detection & Long-Running Worker Tuning]]"
  - "[[Neuron - Eloquent N+1 & Query Plan Optimization]]"
---

# ⚡ Database Performance & Eloquent N+1 Optimization

The single most common cause of slow PHP web applications and API timeouts is the **N+1 Query Problem** and unindexed database queries.

A Senior PHP Developer diagnoses queries using database execution plans (`EXPLAIN ANALYZE`), strict ORM guards, and atomic locking.

---

## 🚫 1. Strict N+1 Prevention

### Automatic Detection in Development:
Instruct your agent to always enable strict models in Laravel:
```php
// In AppServiceProvider.php
public function boot(): void
{
    // Throws an exception in dev/local if an N+1 query is triggered!
    Model::preventLazyLoading(! app()->isProduction());
    Model::preventSilentlyDiscardingAttributes(! app()->isProduction());
    Model::preventAccessingMissingAttributes(! app()->isProduction());
}
```

### Fixing N+1 with Eager Loading:
- ❌ **The Slow Code (1 query + N queries)**:
  ```php
  $posts = Post::latest()->take(20)->get();
  foreach ($posts as $post) {
      echo $post->author->name; // Fires a query for EVERY post! (21 queries total)
  }
  ```
- ✅ **The Senior Fix (2 queries total)**:
  ```php
  $posts = Post::with('author:id,name')->latest()->take(20)->get();
  ```

---

## 🔒 2. Race Conditions & Deadlock Resolution

When two concurrent requests attempt to decrement stock or modify balance:
- ❌ **Unsafe Race Condition**:
  ```php
  $wallet = Wallet::find($id);
  if ($wallet->balance >= $amount) {
      $wallet->balance -= $amount;
      $wallet->save();
  }
  ```
- ✅ **Senior Atomic Update or Pessimistic Lock**:
  ```php
  DB::transaction(function () use ($id, $amount) {
      // SELECT ... FOR UPDATE locks the row until transaction commits
      $wallet = Wallet::where('id', $id)->lockForUpdate()->firstOrFail();
      
      if ($wallet->balance < $amount) {
          throw new InsufficientFundsException();
      }

      $wallet->decrement('balance', $amount);
  }, attempts: 3); // Retries 3 times in case of deadlock!
  ```

---

## 🔍 3. Query Plan Analysis (`EXPLAIN ANALYZE`)
Always inspect slow queries:
```sql
EXPLAIN ANALYZE 
SELECT * FROM orders 
WHERE user_id = 42 AND status = 'completed' 
ORDER BY created_at DESC LIMIT 10;
```
If the plan displays `Seq Scan` (Sequential Table Scan) instead of `Index Scan`, instruct the agent to generate a composite migration:
```php
$table->index(['user_id', 'status', 'created_at']);
```
