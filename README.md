# CLI Cheatsheet System

A static-hosted cheatsheet system with curl-friendly access via custom domain.

## Quick Start

### View Cheatsheets
```bash
curl https://raw.githubusercontent.com/USER/REPO/main/git.txt
curl https://raw.githubusercontent.com/USER/REPO/main/docker.txt
curl https://raw.githubusercontent.com/USER/REPO/main/ssh.txt
curl https://raw.githubusercontent.com/USER/REPO/main/index.txt
```

### Add New Cheatsheet
1. Create a new file named `<topic>.txt`
2. Use the markdown-style format (see format below)
3. Push to main branch
4. Index will auto-generate with git timestamps

## Content Format

Each `.txt` file uses markdown-style formatting:

```
# Category Name
## Command description
actual command here

## Another command description
another command here
```

### Example: `git.txt`
```
# git
## undo last commit
git reset --soft HEAD~1

## interactive rebase last 5
git rebase -i HEAD~5

## force push safely
git push --force-with-lease
```

## Index Format

The `index.txt` is auto-generated with two sections:

```
Recently Modified:
  /docker    (2025-01-29)
  /git       (2025-01-28)
  /ssh       (2025-01-27)

All Topics (by created):
  /git       (2025-01-15)
  /ssh       (2025-01-20)
  /docker    (2025-01-25)
```

## GitHub Pages Setup

1. Go to Settings → Pages
2. Set source to main branch, root directory
3. Configure custom domain (optional)
4. After domain setup, URLs become: `https://c.yourdomain.com/git`

## How It Works

- **GitHub Actions Workflow** (`.github/workflows/generate-index.yml`):
  - Triggers on push to main
  - Scans all `.txt` files
  - Extracts creation and modification dates from git history
  - Generates `index.txt` with sorted listings
  - Auto-commits if index changed

- **GitHub Pages** (`_config.yml`):
  - Includes `.txt` files for serving
  - Enables custom domain routing

## File Structure

```
/
├── .github/
│   └── workflows/
│       └── generate-index.yml
├── git.txt
├── docker.txt
├── ssh.txt
├── index.txt (auto-generated)
├── _config.yml
└── README.md
```

## Contributing

Add new cheatsheets by creating `.txt` files with the standard format. The index will update automatically on push.
