# CLAUDE.md - RateLimiter-KMP

## Overview

`digital.vasic.ratelimiter` is a Kotlin Multiplatform library providing rate limiting utilities: semaphore-based concurrency control, token bucket, adaptive rate limiting, and operation throttling.

**Module**: RateLimiter-KMP (KMP, 4 targets: Android, Desktop/JVM, iOS, Wasm)
**Package**: `digital.vasic.ratelimiter`

## Build & Test

```bash
./gradlew build
./gradlew test                    # All platform tests
./gradlew desktopTest             # Desktop tests only
./gradlew compileKotlinDesktop    # Compile check
```

## Architecture

Single source file with 4 classes, zero internal dependencies beyond kotlinx-coroutines and kotlinx-datetime:

| Class | Purpose |
|-------|---------|
| `RateLimiter` | Semaphore-based concurrent operation limiting |
| `TokenBucket` | Token bucket algorithm with configurable capacity and refill rate |
| `AdaptiveRateLimiter` | Self-adjusting limiter based on success/failure feedback |
| `OperationThrottler` | Per-operation-ID throttling within time windows |

## Code Style

- Kotlin, KMP-compatible (no JVM-only imports)
- Thread safety via `kotlinx.coroutines.sync.Mutex`
- Time via `kotlinx.datetime.Clock.System`
- Tests use `kotlinx.coroutines.test.runTest`
- SPDX Apache-2.0 license headers

## Dependencies

- `kotlinx-coroutines-core` (Semaphore, Mutex, withLock)
- `kotlinx-datetime` (Clock.System for time-based operations)
- Testing: `kotlin-test`, `kotest`, `kotlinx-coroutines-test`

## Design Patterns

- **Decorator**: RateLimitedStorageService wraps storage with rate limiting
- **Strategy**: Different rate limiting strategies (fixed, token bucket, adaptive)

## Commit Style

Conventional Commits: `feat(ratelimiter): add sliding window support`
