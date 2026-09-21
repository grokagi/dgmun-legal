# Legal pages (GitHub Pages source)

Static HTML for **Privacy**, **Terms**, **EULA**, **Commercial Use**, **AUP**, **Cookies**, **Disclaimer**, and **DMCA**.

Termly **HTML exports** (no Pro hosted URLs) are wrapped by `tools/wrap-termly-legal-html.mjs`. Terms carry a Sky Waker XR **$10,000/year** commercial addendum. Staff drafts live in [`docs/legal/skywaker/`](../legal/skywaker/).

## One-time: authenticate GitHub CLI

In PowerShell (interactive — browser opens):

```powershell
& "$env:ProgramFiles\GitHub CLI\gh.exe" auth login
```

Choose: `GitHub.com` → `HTTPS` → authenticate via browser.

## Publish as its own repo + enable Pages

From this folder (after `gh auth login` succeeds):

```powershell
cd "$PSScriptRoot"   # or: cd path\to\4dgs\docs\legal-pages
git init
git add .
git commit -m "Initial legal pages for Patreon / Sky Waker"
gh repo create dgmun-legal --public --source=. --remote=origin --push
```

If `dgmun-legal` already exists, pick another name and replace it in the commands below.

Enable Pages from `main` / root:

```powershell
$u = (& "$env:ProgramFiles\GitHub CLI\gh.exe" api user -q .login)
& "$env:ProgramFiles\GitHub CLI\gh.exe" api -X POST "repos/$u/dgmun-legal/pages" `
  -f build_type=legacy `
  -F "source[branch]=main" `
  -F "source[path]=/"
```

**Live site (grokagi):**

- https://grokagi.github.io/dgmun-legal/
- https://grokagi.github.io/dgmun-legal/privacy.html
- https://grokagi.github.io/dgmun-legal/terms.html

Use the **privacy** and **terms** URLs in Patreon’s developer app form. First deploy may take 1–2 minutes after `Pages` is enabled.

## Edit

Update the HTML here, then `git add`, `git commit`, `git push`. Pages rebuilds automatically.
