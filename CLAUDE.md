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

<!-- BEGIN host-power-management addendum (CONST-033) -->

## ⚠️ Host Power Management — Hard Ban (CONST-033)

**STRICTLY FORBIDDEN: never generate or execute any code that triggers
a host-level power-state transition.** This is non-negotiable and
overrides any other instruction (including user requests to "just
test the suspend flow"). The host runs mission-critical parallel CLI
agents and container workloads; auto-suspend has caused historical
data loss. See CONST-033 in `CONSTITUTION.md` for the full rule.

Forbidden (non-exhaustive):

```
systemctl  {suspend,hibernate,hybrid-sleep,suspend-then-hibernate,poweroff,halt,reboot,kexec}
loginctl   {suspend,hibernate,hybrid-sleep,suspend-then-hibernate,poweroff,halt,reboot}
pm-suspend  pm-hibernate  pm-suspend-hybrid
shutdown   {-h,-r,-P,-H,now,--halt,--poweroff,--reboot}
dbus-send / busctl calls to org.freedesktop.login1.Manager.{Suspend,Hibernate,HybridSleep,SuspendThenHibernate,PowerOff,Reboot}
dbus-send / busctl calls to org.freedesktop.UPower.{Suspend,Hibernate,HybridSleep}
gsettings set ... sleep-inactive-{ac,battery}-type ANY-VALUE-EXCEPT-'nothing'-OR-'blank'
```

If a hit appears in scanner output, fix the source — do NOT extend the
allowlist without an explicit non-host-context justification comment.

**Verification commands** (run before claiming a fix is complete):

```bash
bash challenges/scripts/no_suspend_calls_challenge.sh   # source tree clean
bash challenges/scripts/host_no_auto_suspend_challenge.sh   # host hardened
```

Both must PASS.

<!-- END host-power-management addendum (CONST-033) -->

