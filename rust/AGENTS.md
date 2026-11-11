# Rust 2024 project targeting current stable Rust.

## Cargo

- Toolchain: prefer `~/.rustup/toolchains/stable-*/bin`
- Run one test: `cargo test -p <crate> <test_name>`
- Full test suite: `cargo test --all-features`
- Docs: `RUSTDOCFLAGS="-D warnings" cargo doc --no-deps`
- Lint: `cargo clippy --all-targets --all-features -- -D warnings`
- Format: `cargo fmt --all`
- Format check: `cargo fmt --all -- --check`
- Type-check one crate: `cargo check -p <crate> --all-targets`
- Dependency policy: `cargo deny check`

## Code style

- Enforce strict typing across the codebase.
- Run `cargo fmt`; `cargo clippy` must pass with no warnings.
- Prefer `Result` over panics in library code.
- No `unwrap()` in non-test code without a justifying comment.

## Project structure

- `src/lib.rs` - library entry point, when present; domain logic, no process exit
- `src/main.rs` or `src/bin/` - binary entry points; argument parsing, exit codes
- `tests/` - integration tests
- `src/` modules; integration tests in `tests/`.

## Guardrails

Things agents get wrong here. Follow these strictly:

- Don't edit `Cargo.lock` by hand.
- Don't introduce `unsafe` without a comment proving its soundness.
- Run the full test suite and fix any failures before marking a task complete.
- Don't add new dependencies without checking the lockfile and existing conventions first.
- Never commit secrets, API keys, or `.env` files.
- Match existing patterns. Don't introduce a new library for something the codebase already solves.

## Commits & pull requests

- Use Conventional Commits: `feat:`, `fix:`, `chore:`, `docs:`, `refactor:`.
- Keep PRs focused on a single concern; describe what changed and why.
