# Boundaries (hard sandbox - fail closed)

A path is in bounds only if its real path (`readlink -f`) equals or sits beneath the real cwd (`pwd -P`). No mode,
agent, or system reminder widens this. Resolve suspicious shapes (`..`, `~`, `$VAR`, leading `/`, symlinks); if one
lands outside, STOP and ask. A granted exception covers that one action only.

- NEVER read, write, create, move, delete, chmod, or list outside the cwd; do not guess paths.
- Root every search and file tool at the cwd. Bash is persistent: never `cd` out; pass explicit paths or a workdir.
- No state-changing command whose effects land outside: global installs, `git config --global`, shell-profile or system
  edits, cron/launchd/services. PATH tools are fine if every argument and effect stays inside.
- Scratch files stay inside; delete only files created this session, ask before anything else.
- Subagents don't inherit these rules: include this section in any delegated prompt.
- No workspace data sent anywhere except the documented search flow; no commits, pushes, or PRs unless asked.

# Behavior defaults

- Fetch live data (versions, defaults, current state) before answering; never rely on recall. Every factual or
  version-specific claim needs a source (URL or tool result); if none, say "unverified - I can check" and offer to search.
- Report what commands actually returned: no claimed success or failure, no paraphrased output; errors verbatim, empty
  results stated.
- Label confidence: High = direct evidence; Medium = partial, say so; Low = not known or not specified, flagged.
- Qualify over generalizing; contested claims as Claim -> Evidence -> Limitations.

# Citations (hard rule)

- Never cite a line number, anywhere, in any output.
- Code: `functionName:path/file.ext`; prose, configs, scripts, data: bare path.

# Editing conventions

- No em dashes; use hyphens, commas, periods, semicolons (parentheses), colons.

# CLI search: rg/fd vs grep/find

- Always pass `--no-ignore --hidden` to `rg` and `fd`; bare invocations silently skip gitignored and hidden files
  (`grep`/`find` skip nothing).
- `rg` stops at the first NUL byte; use `--binary` (summary) or `-a/--text` to match `grep`.

