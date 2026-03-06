# RateLimiter-KMP API Reference

## Package: `digital.vasic.ratelimiter`

### class RateLimiter

Semaphore-based rate limiter for concurrent operation control.

| Constructor Parameter | Type | Default | Description |
|-----------------------|------|---------|-------------|
| `maxConcurrent` | `Int` | `5` | Maximum concurrent operations |

| Method | Return Type | Description |
|--------|-------------|-------------|
| `suspend execute(operation)` | `T` | Execute with rate limiting |
| `suspend executeWithTimeout(timeout, operation)` | `T?` | Execute with timeout (ms), null if timed out |
| `suspend getActiveCount()` | `Int` | Current active operations |
| `suspend getQueueLength()` | `Int` | Current queue length |
| `suspend isAtCapacity()` | `Boolean` | True if at max concurrent |

### class TokenBucket

Token bucket algorithm for burst-friendly rate limiting.

| Constructor Parameter | Type | Default | Description |
|-----------------------|------|---------|-------------|
| `capacity` | `Int` | `10` | Maximum tokens |
| `refillRate` | `Double` | `5.0` | Tokens per second |

| Method | Return Type | Description |
|--------|-------------|-------------|
| `suspend tryAcquire()` | `Boolean` | Try to acquire token (non-blocking) |
| `suspend acquire()` | `Unit` | Acquire token (suspends until available) |
| `suspend getAvailableTokens()` | `Int` | Current available tokens |

### class AdaptiveRateLimiter

Self-adjusting rate limiter based on success/failure feedback.

| Constructor Parameter | Type | Default | Description |
|-----------------------|------|---------|-------------|
| `initialRate` | `Int` | `5` | Starting concurrency limit |
| `minRate` | `Int` | `1` | Minimum limit (floor) |
| `maxRate` | `Int` | `20` | Maximum limit (ceiling) |

| Method | Return Type | Description |
|--------|-------------|-------------|
| `suspend execute(operation)` | `T` | Execute with adaptive rate limiting |
| `suspend getCurrentRate()` | `Int` | Current concurrency limit |

### class OperationThrottler

Per-operation-ID throttling within time windows.

| Constructor Parameter | Type | Default | Description |
|-----------------------|------|---------|-------------|
| `windowMs` | `Long` | `1000` | Time window in milliseconds |
| `maxOperations` | `Int` | `10` | Max operations per window |

| Method | Return Type | Description |
|--------|-------------|-------------|
| `suspend tryThrottle(operationId)` | `Boolean` | True if allowed, false if throttled |
| `suspend clear(operationId)` | `Unit` | Clear throttle state for operation |
