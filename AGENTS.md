# AGENTS.md - RateLimiter-KMP

## Agent Capabilities

This module can be used by AI agents for:

1. **Rate limiting API calls** - Prevent overwhelming external services
2. **Concurrency control** - Limit parallel operations in async workflows
3. **Adaptive throttling** - Auto-adjust request rates based on service health
4. **Operation deduplication** - Prevent duplicate operations within time windows

## Integration Points

- Import `digital.vasic.ratelimiter.RateLimiter` for basic concurrency limiting
- Import `digital.vasic.ratelimiter.TokenBucket` for token-based rate limiting
- Import `digital.vasic.ratelimiter.AdaptiveRateLimiter` for self-adjusting limits
- Import `digital.vasic.ratelimiter.OperationThrottler` for per-operation throttling

## Testing

All classes are fully testable with `kotlinx.coroutines.test.runTest`.
