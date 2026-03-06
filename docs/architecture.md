# RateLimiter-KMP Architecture

## Overview

RateLimiter-KMP is a zero-dependency (beyond kotlinx) rate limiting library for Kotlin Multiplatform. It provides four complementary strategies for controlling operation throughput.

## Component Diagram

```
digital.vasic.ratelimiter
├── RateLimiter          (Semaphore-based concurrency control)
├── TokenBucket          (Token bucket algorithm)
├── AdaptiveRateLimiter  (Self-adjusting, wraps RateLimiter)
└── OperationThrottler   (Per-ID time-window throttling)
```

## Dependencies

- `kotlinx-coroutines-core`: Semaphore, Mutex, withLock, delay, withTimeoutOrNull
- `kotlinx-datetime`: Clock.System for time-based operations (TokenBucket, OperationThrottler)

## Design Decisions

1. **Mutex over synchronized**: KMP-compatible, works on all targets
2. **Clock.System over System.currentTimeMillis**: KMP-compatible time source
3. **Semaphore over manual counting**: Built-in backpressure and fairness
4. **Suspend functions throughout**: Natural coroutine integration

## Thread Safety Model

All mutable state is protected by `kotlinx.coroutines.sync.Mutex`. The `RateLimiter` additionally uses `kotlinx.coroutines.sync.Semaphore` for permit management.

## Relationships

- `AdaptiveRateLimiter` composes a `RateLimiter` internally
- All other classes are independent and can be used standalone
