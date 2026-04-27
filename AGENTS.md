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

<!-- BEGIN host-power-management addendum (CONST-033) -->

## Host Power Management — Hard Ban (CONST-033)

**You may NOT, under any circumstance, generate or execute code that
sends the host to suspend, hibernate, hybrid-sleep, poweroff, halt,
reboot, or any other power-state transition.** This rule applies to:

- Every shell command you run via the Bash tool.
- Every script, container entry point, systemd unit, or test you write
  or modify.
- Every CLI suggestion, snippet, or example you emit.

**Forbidden invocations** (non-exhaustive — see CONST-033 in
`CONSTITUTION.md` for the full list):

- `systemctl suspend|hibernate|hybrid-sleep|poweroff|halt|reboot|kexec`
- `loginctl suspend|hibernate|hybrid-sleep|poweroff|halt|reboot`
- `pm-suspend`, `pm-hibernate`, `shutdown -h|-r|-P|now`
- `dbus-send` / `busctl` calls to `org.freedesktop.login1.Manager.Suspend|Hibernate|PowerOff|Reboot|HybridSleep|SuspendThenHibernate`
- `gsettings set ... sleep-inactive-{ac,battery}-type` to anything but `'nothing'` or `'blank'`

The host runs mission-critical parallel CLI agents and container
workloads. Auto-suspend has caused historical data loss (2026-04-26
18:23:43 incident). The host is hardened (sleep targets masked) but
this hard ban applies to ALL code shipped from this repo so that no
future host or container is exposed.

**Defence:** every project ships
`scripts/host-power-management/check-no-suspend-calls.sh` (static
scanner) and
`challenges/scripts/no_suspend_calls_challenge.sh` (challenge wrapper).
Both MUST be wired into the project's CI / `run_all_challenges.sh`.

**Full background:** `docs/HOST_POWER_MANAGEMENT.md` and `CONSTITUTION.md` (CONST-033).

<!-- END host-power-management addendum (CONST-033) -->

