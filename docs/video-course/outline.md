# RateLimiter-KMP Video Course Outline

## Episode 1: Introduction to Rate Limiting
- Why rate limiting matters
- Common strategies: fixed window, sliding window, token bucket, semaphore
- Overview of RateLimiter-KMP

## Episode 2: RateLimiter - Semaphore-Based Concurrency Control
- How semaphores work in Kotlin coroutines
- Using RateLimiter to limit concurrent API calls
- Timeout handling with executeWithTimeout
- Monitoring active operations

## Episode 3: TokenBucket - Burst-Friendly Rate Limiting
- Token bucket algorithm explained
- Configuring capacity and refill rate
- Non-blocking vs suspending acquisition
- Real-world API rate limit scenarios

## Episode 4: AdaptiveRateLimiter - Self-Adjusting Limits
- Feedback-driven rate adjustment
- Success/failure thresholds
- Min/max rate bounds
- Use cases: cloud services with variable capacity

## Episode 5: OperationThrottler - Per-Operation Control
- Time-window based throttling
- Operation ID grouping
- Preventing UI event flooding
- Clearing throttle state
