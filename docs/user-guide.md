# RateLimiter-KMP User Guide

## Introduction

RateLimiter-KMP provides four rate limiting strategies for Kotlin Multiplatform applications. All implementations are thread-safe and coroutine-compatible.

## RateLimiter

Limits concurrent operations using a semaphore.

```kotlin
val limiter = RateLimiter(maxConcurrent = 3)

// Basic usage
val result = limiter.execute { fetchData() }

// With timeout (returns null if timed out)
val result = limiter.executeWithTimeout(5000) { fetchData() }

// Monitoring
val active = limiter.getActiveCount()
val queued = limiter.getQueueLength()
val full = limiter.isAtCapacity()
```

## TokenBucket

Allows burst traffic while maintaining an average rate.

```kotlin
val bucket = TokenBucket(capacity = 10, refillRate = 5.0)

// Non-blocking check
if (bucket.tryAcquire()) {
    callApi()
}

// Suspending wait
bucket.acquire() // waits until token available

// Check availability
val tokens = bucket.getAvailableTokens()
```

## AdaptiveRateLimiter

Automatically adjusts concurrency based on operation outcomes.

```kotlin
val limiter = AdaptiveRateLimiter(
    initialRate = 5,
    minRate = 1,
    maxRate = 20
)

val result = limiter.execute { callApi() }
// After 10+ successes: rate increases by 1
// After 3+ failures: rate decreases by 1

val currentRate = limiter.getCurrentRate()
```

## OperationThrottler

Prevents flooding by limiting operations per time window, grouped by ID.

```kotlin
val throttler = OperationThrottler(
    windowMs = 1000,
    maxOperations = 10
)

if (throttler.tryThrottle("user-search")) {
    performSearch()
} else {
    showRateLimitMessage()
}

// Reset throttle for an operation
throttler.clear("user-search")
```

## Thread Safety

All classes use `kotlinx.coroutines.sync.Mutex` for thread safety. They are safe to use from multiple coroutines concurrently.
