# Go project.

## Go

- Install deps: `go mod download`; sync after edits: `go mod tidy`
- Build: `go build ./...`
- Run tests: `go test ./...`
- Apply modernizations: `go fix ./...`
- Lint / format: `golangci-lint run`
- Check: `test -z "$(gofmt -l .)"`, `go fix -diff ./...`, `go vet ./...`, `go test -race -shuffle=on ./...`

## Code style

- Prefer concrete types and narrow interfaces over `any` in exported APIs.
- Run `gofmt`; code must be formatted before commit.
- Handle every error explicitly - never use `_` to discard one.
- Keep packages small and focused.
- No bare type assertion `x.(T)`; use `v, ok := x.(T)` and handle `!ok`.
- No `panic`, `log.Fatal`, or `os.Exit` outside `main`; return `error`.
- Every `go` statement has a defined exit condition (closed channel, cancelled ctx) and the
  spawner waits: `wg.Wait()` or `errgroup`.

## Project structure

- `cmd/` for entrypoints, `internal/` for private packages.

## Guardrails

Things agents get wrong here. Follow these strictly:

- Don't edit `go.mod` or `go.sum` by hand; use `go get` / `go mod tidy`.
- Run the full test suite and fix any failures before marking a task complete.
- Use the standard library first; don't add a dependency it already covers.
- Don't add new dependencies without checking `go.mod` / `go.sum` and existing conventions first.
- Never commit secrets, API keys, or `.env` files.
- Match existing patterns. Don't introduce a new library for something the codebase already solves.

## Commits & pull requests

- Use Conventional Commits: `feat:`, `fix:`, `chore:`, `docs:`, `refactor:`.
- Keep PRs focused on a single concern; describe what changed and why.
