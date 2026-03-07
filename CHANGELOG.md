<!-- SPDX-FileCopyrightText: 2025 Milos Vasic -->
<!-- SPDX-License-Identifier: Apache-2.0 -->

# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-03-06

### Added
- Initial release extracted from Yole monolith
- `RateLimiter` - Semaphore-based concurrent operation limiting with configurable max concurrency
- `TokenBucket` - Token bucket algorithm for burst-friendly rate limiting with configurable capacity and refill rate
- `AdaptiveRateLimiter` - Self-adjusting rate limiter that adapts based on success/failure feedback
- `OperationThrottler` - Per-operation-ID throttling within configurable time windows
- Kotlin Multiplatform support (Android, Desktop/JVM, iOS, Wasm/JS)
- Comprehensive test suite
- CI/CD via GitHub Actions

### Infrastructure
- Gradle build with version catalog
- Kover code coverage
- SPDX license headers (Apache-2.0)
