# Real time stock ticker static

Simple static project that contains a single file:

- `stock.html` — the main (and only) file. Open it in your browser to view the real-time stock ticker demo.

## How to run

1. Open the project folder in File Explorer.
2. Double-click `stock.html` or open it from your browser (File → Open File).

No server or build step required — it's a plain static HTML file.

## Files

- `stock.html` — stock ticker demo.

## GitHub: Upload / Push notes

If you saw this error when running `git fetch` or `git push`:

```
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

This means SSH authentication with GitHub isn't set up or the SSH key isn't added to your GitHub account. You have two quick options:

### Option A — Quick workaround: use HTTPS remote (fast)

Replace the remote URL to use HTTPS and push. In PowerShell run:

```powershell
# check remotes
git remote -v

# set the origin (or the remote name you use) to HTTPS
# Replace USERNAME/REPO with your repo path
git remote set-url origin https://github.com/USERNAME/REPO.git

# stage and push
git add .
git commit -m "Add README"
git push origin main
```

If your branch is named `master` or another name, use that instead of `main`. If your remote isn't named `origin` (for example you used `New`), replace `origin` with that remote name.

### Option B — Proper fix: set up SSH keys (preferred long-term)

1. Generate an SSH key (use your email):

```powershell
# recommended: ed25519 (if supported)
ssh-keygen -t ed25519 -C "your_email@example.com"
# or fallback to RSA if ed25519 isn't available
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Accept the default file locations (press Enter), and optionally supply a passphrase.

2. Start the ssh-agent and add the key (PowerShell):

```powershell
# start the agent as a service (Windows 10/11)
Start-Service ssh-agent
# add your private key (adjust filename if you used rsa)
ssh-add $env:USERPROFILE\.ssh\id_ed25519
```

3. Copy the public key to the clipboard and add it to GitHub:

```powershell
Get-Content $env:USERPROFILE\.ssh\id_ed25519.pub | clip
```

- Go to https://github.com → Settings → SSH and GPG keys → New SSH key. Paste the key and save.

4. Test the connection:

```powershell
ssh -T git@github.com
```

You should see a welcome message from GitHub confirming authentication. If you still get `Permission denied (publickey)`, ensure your key is added to the agent and to your GitHub account.

### Check remote name

If you used a remote name called `New` (as in `git fetch New`), list remotes and update that specific remote:

```powershell
git remote -v
# replace 'New' with HTTPS (if using Option A)
git remote set-url New https://github.com/USERNAME/REPO.git
```

## Notes and next steps

- Replace `USERNAME/REPO` with your GitHub username and repository name.
- If you want, I can:
  - update the remote URL in your repo for you, or
  - generate the README with additional screenshots or usage notes.

---

Created automatically. If you'd like a shorter README or one tailored for GitHub Pages, tell me how you'd like it formatted.