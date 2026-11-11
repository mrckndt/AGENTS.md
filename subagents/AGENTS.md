# Model and effort selection for delegated work

## Model tiers

- Map `{{cheap-model}}` and `{{strong-model}}` to the models the harness offers.
- Rewrite or extend the examples below for the project.

### Mechanical tier - `{{cheap-model}}`

- Search and exploration fan-out.
- Summarizing known files.
- Boilerplate and mechanical refactors.
- Tests against a clear spec.
- Small, well-specified changes.
- {{add project-specific mechanical work here}}

### Reasoning tier - `{{strong-model}}`

- Code review.
- Bugs with an unknown cause.
- Ambiguous tasks or ones that need wide context.
- Architecture and cross-cutting design.
- Concurrency, state or security bugs.
- Reviews of risky changes.
- {{add project-specific judgment-heavy work here}}

## Effort and thinking

- Set it explicitly when the harness exposes it.
- Mechanical work: `{{default-effort}}`, the model's default level.
- Reasoning-heavy work: `{{high-effort}}`, above the default.
- Not every model supports it, and the level names differ by provider.
- Keep model and effort fixed for the duration of a task; changing either mid-run discards prompt cache and prior work.
- Mapping: OpenCode `provider/model#variant`; Claude Code `/effort` or `effortLevel`.

## Dispatch hygiene

- A brief states the objective, scope (files or subsystem), constraints and output format.
  Subagents (except forks) do not inherit your context.
- Every report ends with a confidence level (high, medium or low) and any open doubts.
- Check every result yourself: run the tests or read the diff.
- Run subagents in parallel only on independent problems with disjoint files.
