# File Scanner Pro

A JavaScript bookmarklet for bug bounty hunters and penetration testers to scan web servers for exposed sensitive files, misconfigurations, and information leaks.

## Features

- **250+ paths** — scans common sensitive files: `.env`, `.git/config`, `wp-config.php`, cloud credentials, backup files, logs, and more
- **100+ signatures** — detects credentials, API keys, tokens, database strings, private keys, and configuration leaks
- **Soft-404 detection** — builds a baseline fingerprint of your target's 404 page to filter out false positives
- **Concurrent scanning** — checks 8 paths simultaneously for speed
- **Results UI** — color-coded overlay with copy, export (JSON), and direct link actions
- **Zero dependencies** — pure vanilla JavaScript, runs in any modern browser

## Usage

### Option 1: Bookmarklet (drag & drop)

1. Create a new bookmark in your browser
2. Set the name to `File Scanner Pro`
3. Set the URL to the minified code from [`bookmarklet.min.js`](./bookmarklet.min.js)

### Option 2: Browser console

1. Open the target website
2. Open browser DevTools (F12)
3. Paste the contents of [`filescanner-pro.js`](./filescanner-pro.js) into the console
4. Press Enter

The scanner will instantly begin probing paths and display results in a floating overlay.

## Results

| Color | Label | Meaning |
|-------|-------|---------|
| 🔴 Red | `SENSITIVE` | File contains credentials, keys, or sensitive data |
| 🟡 Yellow | `FORBIDDEN` | Path returns 401/403 — exists but protected |
| 🟢 Green | `OPEN` | File is publicly accessible |
| ⚪ Gray | `OPEN?` | Accessible but very small, likely benign |

## Detection signatures

The scanner looks for:
- **Database credentials** — `DB_PASSWORD`, `DATABASE_URL`, `MYSQL_PASSWORD`, `POSTGRES_PASSWORD`
- **Cloud keys** — `AWS_ACCESS`, `AKIA`, `AZURE_CLIENT`, `AZURE_STORAGE`, `"type": "service_account"`
- **API tokens** — `sk_live_`, `ghp_`, `xoxb-`, `github_pat_`, `access_token`
- **Private keys** — `-----BEGIN RSA PRIVATE KEY-----`, `-----BEGIN OPENSSH PRIVATE KEY-----`
- **Framework secrets** — `APP_KEY`, `JWT_SECRET`, `SECRET_KEY`, `ENCRYPTION_KEY`
- **Configuration** — `[core]`, `repositoryformatversion`, `phpinfo()`, `apiVersion`
- **Infrastructure** — `kind: Secret`, `kind: Deployment`, `terraform.tfvars`

## Disclaimer

This tool is intended for **authorized security testing only**. Unauthorized scanning of web servers may violate laws and terms of service. The author is not responsible for misuse.

## Author

**Burhan ALDeen** — v4.1
