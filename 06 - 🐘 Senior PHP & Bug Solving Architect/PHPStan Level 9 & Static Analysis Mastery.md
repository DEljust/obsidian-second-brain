---
title: PHPStan Level 9 & Static Analysis Mastery
tags:
  - php
  - phpstan
  - static-analysis
  - type-safety
  - bug-solving
github_repos:
  - https://github.com/phpstan/phpstan
  - https://github.com/larastan/larastan
related_notes:
  - "[[Senior PHP Bug Solving & Architecture Blueprint]]"
  - "[[Xdebug 3 & AI Agent MCP Debugging (koriym-xdebug-mcp)]]"
  - "[[Complete Senior PHP & Bug Solving .cursorrules]]"
  - "[[Neuron - PHPStan Level 9 Static Analysis]]"
---

# 🔍 PHPStan Level 9 & Static Analysis Mastery

A Senior PHP Developer uses static analysis to prevent 95% of runtime crashes—especially `TypeError`, `Call to a member function on null`, and undefined array key notices—before code ever reaches staging.

---

## 📊 The Strictness Hierarchy

```mermaid
graph TD
    L0["Level 0-2: Basic syntax, missing classes & unknown methods"]
    L3["Level 3-5: Return types, dead code, method signatures"]
    L6["Level 6-7: Missing typehints, union type consistency"]
    L8["Level 8: Null-safe checking (Calling methods on nullable types forbidden)"]
    L9["Level 9 / MAX: Absolute Type Certainty (Zero implicit 'mixed' types allowed)"]

    L0 --> L3 --> L6 --> L8 --> L9
    classDef senior fill:#1e3a8a,stroke:#60a5fa,color:#fff;
    class L8,L9 senior;
```

---

## 🛑 Common Anti-Patterns & Senior Solutions

### 1. The `Call to a member function on null` Bug
- ❌ **Junior Code**:
  ```php
  $user = User::find($id);
  return $user->email; // Crash if $user is null
  ```
- ✅ **Senior Level 9 Fix**:
  ```php
  $user = User::findOrFail($id); // Throws ModelNotFoundException
  // OR explicit narrowing:
  $user = User::find($id);
  if ($user === null) {
      throw new ResourceNotFoundException("User {$id} does not exist.");
  }
  return $user->email;
  ```

### 2. Eliminating `mixed` in Collections & Generics
- ❌ **Junior Code**:
  ```php
  public function getOrders(): array { ... }
  ```
- ✅ **Senior Level 9 Fix (Generics via PHPDoc)**:
  ```php
  /**
   * @return array<int, OrderDTO>
   */
  public function getOrders(): array { ... }
  ```

### 3. Exhaustive Enums & Match Expressions
When handling state machines, PHPStan verifies all Enum cases are handled:
```php
enum PaymentStatus: string {
    case Pending = 'pending';
    case Completed = 'completed';
    case Failed = 'failed';
    case Refunded = 'refunded';
}

// PHPStan Level 9 throws an error if ANY case is omitted without a default!
return match ($status) {
    PaymentStatus::Pending => $this->handlePending(),
    PaymentStatus::Completed => $this->handleSuccess(),
    PaymentStatus::Failed => $this->handleFailure(),
    PaymentStatus::Refunded => $this->handleRefund(),
};
```

---

## ⚙️ Recommended `phpstan.neon` Configuration
```neon
includes:
    - vendor/larastan/larastan/extension.neon # or symfony extension

parameters:
    level: 9
    paths:
        - app
        - src
        - tests
    checkGenericClassInNonGenericObjectType: true
    checkMissingIterableValueType: true
    treatPhpDocTypesAsCertain: false
```
