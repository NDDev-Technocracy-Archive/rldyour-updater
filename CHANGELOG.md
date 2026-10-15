# Changelog

## [0.2.2] - 2026-10-15

- Keep bounded installer stdout/stderr and the child exit code on
  receipt-parse and receipt-contract failures; both paths previously reported
  "installer did not produce a valid structured receipt" while discarding the
  only diagnostic evidence.
- Accept relative paths for the catalogue build/sign/verify CLI arguments;
  they are resolved against the working directory before the strict
  absolute-path storage boundary.
- Refresh the catalogue keys README: the nddev anchor rotation already
  executed at sequence 3 and the status table now reflects it.

## [0.2.1] - 2026-10-08

- Qualify scheduled signed update transactions on native Ubuntu and macOS.
- Handle bounded Homebrew backlogs, unhashable native-update casks and real exit codes.
- Explicitly release native locks, expose bundled rustdoc, and keep nightly
  updates free of PyTorch imports or GPU initialization.
- Publish Linux x86_64 and macOS arm64 raw binaries with checksums for signed
  catalogue self-updates.

## [0.2.0] - 2026-10-08

- Authenticate an expiring Ed25519 catalogue with exact source SHA256/lengths,
  monotonic release sequence and durable anti-rollback/equivocation state.
- Execute verified private source snapshots; stop trusting mutable checkouts or
  arbitrary legacy argv. Add offline catalogue build/sign/verify commands.
- Add separate root-owned installed desktop/DEB update transactions and optional
  native Homebrew/Flatpak providers with clear update ownership.
- Retain real exit codes, exact CLI change receipts and unknown partial outcomes.
- Bound storage/lock/report paths and sizes, private atomic publication, process
  groups and Windows Job Objects. Add synthetic security/transaction regression tests.

## [0.1.0] - 2026-10-08

- Initial coordinator, policy/plan/status commands, GDS bootstrap invocation,
  APT observation and daily Linux/macOS user scheduling.
