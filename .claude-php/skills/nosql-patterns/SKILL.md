---
name: nosql-patterns
description: NoSQL best practices for PHP and Laravel. Use when working with Redis (Caching/Sessions), MongoDB, or designing high-performance NoSQL data stores.
---

# NoSQL Patterns Skill (PHP/Laravel)

Efficiently working with non-relational databases in modern PHP/Laravel applications.

## When to Use
- Implementing high-performance caching strategies using Redis.
- Managing PHP sessions or distributed locking in Redis.
- Integrating MongoDB with Laravel using `php-mongodb` or specialized packages.

---

## Redis (Caching & Sessions)

### Use Case: Distributed Locking
```php
use Illuminate\Support\Facades\Redis;

$lock = Redis::lock('processing_order_123', 10);
if ($lock->get()) {
    // Process order...
    $lock->release();
}
```

### Best Practices
- **Tags**: Use Laravel's cache tags (`Cache::tags(['people', 'artists'])->put(...)`) for groups of related data if supported by the driver (Redis).
- **Atomic Operations**: Use Redis atomic increments/decrements for counters.
- **Prefixing**: Ensure `prefix` in `config/database.php` is set for Redis multi-tenant environments.

---

## MongoDB (Laravel)

### Model Configuration
Laravel doesn't support MongoDB out of the box, but `mongodb/laravel-mongodb` is the standard.
```php
use MongoDB\Laravel\Eloquent\Model;

class Post extends Model
{
    protected $connection = 'mongodb';
}
```

## Best Practices
- **Hybrid Storage**: Use SQL (MariaDB/Postgre) for relational data and NoSQL (MongoDB) for unstructured logs or dynamic attributes.
- **Serialization**: Ensure proper handling of `ObjectID` vs string IDs when returning JSON.
- **Performance**: Monitor memory usage when fetching large document sets into Eloquent Models.
