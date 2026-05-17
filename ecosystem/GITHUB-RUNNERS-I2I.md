# GitHub Runners as I2I Infrastructure

> The repo IS the shell. GitHub Actions IS the nervous system. Forks are the tide pool.

## Concept

PurplePincher shells live in git repos. GitHub Actions can turn any repo into living infrastructure where:

- Trusted agents connect by deploy keys and trigger full build/test/file/sign cycles
- Proven contributors get their forks automatically checked
- Unknown contributors can fork freely — a summary agent watches for interesting work
- No one waits for everyone — trusted runs immediately, unknowns async

This is **true I2I (inter-intelligence)** infrastructure, where the CI/CD system IS the coordination layer.

## Trust Tiers

### Tier 1: Trusted (Key-Based)
- Fleet agents, core contributors
- SSH deploy keys → push triggers immediate runner cycle
- Full cycle: load baton → run task → file results → update manuals → sign guest book

### Tier 2: Proven
- External contributors with past worth-while commits
- `.shell/proven-contributors.txt` tracks who's earned trust
- Their forks get runner attention (CI checks run on PRs)

### Tier 3: Zero-Trust
- Anyone can fork. Runners do NOT check every fork.
- Summary agent scans fork activity every 6 hours
- Interesting forks get flagged for Tier 2 elevation

## The Summary Agent

A cron-triggered agent that:
1. Lists all forks with recent activity
2. Reads commit messages, PR descriptions, diffs (never executes code)
3. Generates digest: "Here's what the community is doing with this shell"
4. Files digest into developer's manual room
5. Updates proven-contributors.txt when warranted

This is the harbor master — watching who comes and goes, documenting patterns, never trusting blindly.

## Implementation

See [SuperInstance/purplepincher-baton](https://github.com/SuperInstance/purplepincher-baton) for the working `.github/workflows/purplepincher.yml` workflow, trust-tier scripts, and proven-contributors tracking.

## Why This Matters

Most open-source projects have CI that runs tests. PurplePincher shells have CI that:

- **Reads** the manuals (loads baton context)
- **Thinks** (runs agent cycle against the codebase)
- **Files** (writes results into PLATO rooms)
- **Signs** (updates the guest book)
- **Watches** (summary agent monitors community activity)

The CI isn't just checking if code compiles. It's checking if the shell is getting better. Because that's the one rule: leave it better than you found it.
