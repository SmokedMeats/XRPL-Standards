# XRP Ledger Standards

XRP Ledger Standards (XLSs) describe standards and specifications relating to the XRP Ledger ecosystem that help achieve the following goals:

- Ensure interoperability and compatibility between XRP Ledger core protocol, ecosystem applications, tools, and platforms.
- Maintain a continued, excellent user experience around every application or system.
- Drive alignment and agreement in the XRPL community (i.e., developers, users, operators, etc).

# [Contributing](./CONTRIBUTING.md)

The exact process for organizing and contributing to this repository is defined in [CONTRIBUTING.md](./CONTRIBUTING.md). If you would like to contribute, please read more there.
## Before pushing (this fork)

This fork is public. Every push runs a local `check:public-safe` gate (no CI minutes): [gitleaks](https://github.com/gitleaks/gitleaks) over the commits being pushed, then a private denylist over every added line, new file path, and commit message in those commits.

One-time setup per clone:

```bash
git config core.hooksPath .githooks
# gitleaks: brew install gitleaks | winget install gitleaks | scoop install gitleaks | release binary on Linux
# The private denylist is found via $PUBLIC_SAFE_DENYLIST, `git config publicsafe.denylist`,
# or a sibling clone carrying public-safe/denylist.txt. Missing denylist = push blocked.
```

Run it by hand (needs Node 18+; works in bash, Git Bash, and PowerShell):

```bash
node scripts/check-public-safe.mjs              # origin default branch..HEAD
node scripts/check-public-safe.mjs --base <ref> # <ref>..HEAD, e.g. a stacked PR
node scripts/check-public-safe.mjs --tree       # whole tracked tree at HEAD (audit)
```

A clean run prints one line, e.g. `check:public-safe PASS <repo>@<sha> (gitleaks 0, denylist 0)`. Paste that line in the PR body.

