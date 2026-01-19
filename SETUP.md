# Setup Instructions

After forking/cloning this template, follow these steps:

## ✅ Checklist

- [ ] Make your fork **PRIVATE** (Settings → Danger Zone → Change visibility)
- [ ] Add 3 GitHub Secrets (Settings → Secrets → Actions):
  - [ ] `GMAIL_APP_PASSWORD`
  - [ ] `BENEFICIARY_EMAIL`
  - [ ] `VAULT_PASSWORD`
- [ ] Edit `.github/workflows/deadman.yml` line 43 with your Gmail
- [ ] Replace `REPLACE_WITH_YOUR_GITHUB_REPO_URL` in workflow file (lines 84, 90, 93)
- [ ] Create encrypted vault files in `vault/` folder
- [ ] Test the workflow (Actions tab → Run workflow)
- [ ] Change threshold from 0 to 49 in workflow (line 26) after testing
- [ ] Do your first check-in (update status.txt)

See README.md for detailed instructions!
