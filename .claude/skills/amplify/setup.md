# amplify setup

## Prerequisites

- **gh CLI** — GitHub's command-line tool
- **git** — version control (usually pre-installed)

## Quick check

Run these to verify setup:

```bash
gh --version     # Should show gh version X.Y.Z
gh auth status   # Should show "Logged in to github.com"
git --version    # Should show git version X.Y.Z
```

## Install gh CLI

**macOS:**

```bash
brew install gh
```

**Linux:**

```bash
# Debian/Ubuntu
sudo apt install gh

# Fedora
sudo dnf install gh
```

**Windows:**

```bash
winget install GitHub.cli
```

Or download from [cli.github.com](https://cli.github.com).

## Authenticate

```bash
gh auth login
```

Follow the prompts — choose GitHub.com, HTTPS, and authenticate via browser.

## Verify

```bash
gh auth status
```

You should see your username and the scopes granted. You're ready to use
amplify.
