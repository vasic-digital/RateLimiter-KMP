# RateLimiter-KMP

Kotlin Multiplatform rate limiting library providing semaphore-based concurrency control, token bucket, adaptive rate limiting, and operation throttling.

## Features

- **RateLimiter** - Semaphore-based concurrent operation limiting
- **TokenBucket** - Token bucket algorithm for burst-friendly rate limiting
- **AdaptiveRateLimiter** - Self-adjusting rate limiter based on success/failure feedback
- **OperationThrottler** - Per-operation-ID throttling within time windows

## Platforms

| Platform | Status |
|----------|--------|
| Android | Supported |
| Desktop (JVM) | Supported |
| iOS | Supported |
| Web (Wasm) | Supported |

## Installation

### Gradle (Composite Build)

```kotlin
// settings.gradle.kts
includeBuild("RateLimiter-KMP")

// build.gradle.kts
dependencies {
    implementation("digital.vasic.ratelimiter:RateLimiter-KMP")
}
```

## Quick Start

```kotlin
import digital.vasic.ratelimiter.RateLimiter

// Limit to 3 concurrent operations
val limiter = RateLimiter(maxConcurrent = 3)
val result = limiter.execute { fetchData() }

// Token bucket for API rate limiting
val bucket = TokenBucket(capacity = 10, refillRate = 5.0)
if (bucket.tryAcquire()) { callApi() }

// Adaptive rate limiting
val adaptive = AdaptiveRateLimiter(initialRate = 5)
val data = adaptive.execute { callApi() } // auto-adjusts on success/failure

// Operation throttling
val throttler = OperationThrottler(windowMs = 1000, maxOperations = 10)
if (throttler.tryThrottle("api-call")) { proceed() }
```

## License

Apache-2.0
