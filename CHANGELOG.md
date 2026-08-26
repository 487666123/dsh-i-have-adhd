# Changelog

## 1.0.0 (2026-08-26)

- Renamed from dsh-i-have-adhd before any dependent users existed; the
  earlier name published a deprecated 1.0.1 pointing here.

Initial release.

- One system-prompt section (`dsh-ihaveadhd`, order 50) carrying a from-scratch ADHD-friendly output ruleset (Shape / State / Tone, ten ideas plus harness-aware overrides).
- `adhd_on` / `adhd_off` / `adhd_status` agent tools with flag-file persistence under `$DSH_HOME/dsh-ihaveadhd/always-on`; boot restores the persisted mode.
- Originality smoke gate: seventeen distinctive upstream phrases (ayghri/i-have-adhd) are asserted absent from the ruleset; concept coverage, interpolation safety and the full state machine are tested against a mocked Cordis context.
