# Dead Man's Switch - Emergency Data Vault

A **free, zero-cost** automated emergency backup system that monitors your activity and sends encrypted data to a trusted beneficiary if you don't check in for 49 hours.

## Features

- ✅ **Completely Free** - Uses GitHub Actions (2,000 minutes/month free)
- ✅ **Zero Maintenance** - Automated hourly checks
- ✅ **Secure** - AES-256 encrypted vault files
- ✅ **Private** - Runs in your private GitHub repository
- ✅ **Simple Check-In** - Just commit a file every 48 hours
- ✅ **Non-Technical Friendly** - Clear instructions for beneficiaries

## 🎯 How It Works

```
┌─────────────────┐
│ Every Hour:     │
│ GitHub Actions  │──> Checks last commit to status.txt
│ runs workflow   │
└─────────────────┘
         │
         ├─> Less than 49 hours? ✅ Do nothing
         │
         └─> More than 49 hours? 🚨 Send emergency email
                                     with vault password
```

## Quick Start (15 Minutes Setup)

### Prerequisites
- GitHub account (free)
- Gmail account (for sending emails)
- 7-Zip installed (for encryption)

### Step 1: Fork This Repository

1. Click the **"Use this template"** button (or Fork)
2. Make it **PRIVATE** ⚠️ (very important!)
3. Name it whatever you like (e.g., `my-emergency-vault`)

### Step 2: Configure GitHub Secrets

Go to: `Settings → Secrets and Variables → Actions → New repository secret`

Add these **3 secrets**:

| Secret Name | Description | Example |
|------------|-------------|---------|
| `GMAIL_APP_PASSWORD` | Gmail app password ([how to get](https://support.google.com/accounts/answer/185833)) | `abcd efgh ijkl mnop` |
| `BENEFICIARY_EMAIL` | Email of trusted person | `trusted@example.com` |
| `VAULT_PASSWORD` | Password for encrypted files | `MyStr0ngP@ssw0rd!` |

### Step 3: Update Workflow File

Edit `.github/workflows/deadman.yml` line 43:

```yaml
user: YOUR_GMAIL_ADDRESS@gmail.com
```

Replace with your actual Gmail address.

### Step 4: Encrypt Your Important Files

```bash
# Install 7-Zip first: https://www.7-zip.org/

# Encrypt your files (Windows)
& "C:\Program Files\7-Zip\7z.exe" a -p"YOUR_PASSWORD" -mhe=on -mx=9 ".\vault\emergency-vault.7z" ".\your-important-files.txt"

# Encrypt your files (Mac/Linux)
7z a -p"YOUR_PASSWORD" -mhe=on -mx=9 "./vault/emergency-vault.7z" "./your-important-files.txt"
```

⚠️ Use the same password as your `VAULT_PASSWORD` secret!

### Step 5: Test It!

1. Go to `Actions` tab
2. Click `49-Hour Emergency Monitor`
3. Click `Run workflow`
4. Check if the beneficiary receives the email

### Step 6: Restore Production Settings

⚠️ **IMPORTANT:** After testing, change threshold back to 49 hours!

Edit `.github/workflows/deadman.yml` line 26:
```yaml
if [ $DIFF_HOURS -ge 49 ]; then  # Change from 0 to 49
```

### Step 7: Initial Check-In

```bash
# Update status file
echo "Last check-in: $(date)" > status.txt
git add status.txt
git commit -m "Check-in: $(date)"
git push
```

## 🔄 How to Check In (Every 48 Hours)

**Option 1: Manual (GitHub Web)**
1. Go to your repository
2. Edit `status.txt`
3. Change the date
4. Commit directly to main

**Option 2: Command Line**
```bash
echo "Last check-in: $(date)" > status.txt
git add status.txt
git commit -m "Check-in"
git push
```

**Option 3: Automate It** (optional)
Set up a reminder on your phone/calendar for every 48 hours.

## 📧 What Your Beneficiary Receives

When triggered, they get an email with:
- ✅ The vault password (clearly highlighted)
- ✅ Step-by-step instructions to access files
- ✅ Links to detailed guides
- ✅ Warnings about common mistakes
- ✅ Troubleshooting tips

See `vault/HOW-TO-OPEN.md` for the beneficiary guide.

## 🔐 Security Features

- **AES-256 Encryption** - Military-grade encryption for vault files
- **Private Repository** - Only you and GitHub can see your data
- **Password Protected** - Files require password to decrypt
- **No Cloud Service** - Your files stay in your GitHub repo
- **Header Encryption** - Even filenames are encrypted in .7z

## 📁 Repository Structure

```
deadmanswitch/
├── .github/workflows/
│   └── deadman.yml          # The automation brain
├── vault/
│   ├── emergency-vault.7z   # Your encrypted files (you create this)
│   ├── HOW-TO-OPEN.md       # Detailed beneficiary instructions
│   └── QUICK-START.txt      # Printable quick reference
├── status.txt               # Your check-in file
├── .gitignore
└── README.md
```

## 🎨 Customization

### Change the Time Threshold

Edit line 26 in `.github/workflows/deadman.yml`:
```yaml
if [ $DIFF_HOURS -ge 49 ]; then  # Change 49 to your preferred hours
```

### Change Email Content

Edit the email template in `.github/workflows/deadman.yml` starting at line 55.

### Add More Vault Files

```bash
7z a -p"YOUR_PASSWORD" -mhe=on "./vault/documents.7z" "./my-documents/*"
7z a -p"YOUR_PASSWORD" -mhe=on "./vault/passwords.7z" "./passwords.txt"
```

## 🆘 Troubleshooting

### "Workflow isn't running"
- Make sure the repository is private
- Check that GitHub Actions are enabled in Settings
- Verify all 3 secrets are set correctly

### "Email not sending"
- Verify Gmail App Password is correct (not your regular password)
- Check beneficiary email is correct
- Look at workflow logs for error messages

### "Beneficiary can't open files"
- Send them: https://github.com/YOUR-USERNAME/YOUR-REPO/blob/main/vault/HOW-TO-OPEN.md
- Make sure they're RIGHT-CLICKING, not double-clicking
- Verify they installed 7-Zip from https://www.7-zip.org/

## ⚠️ Important Warnings

1. **Keep Repository Private** - Don't make it public!
2. **Test Before Relying On It** - Make sure emails actually arrive
3. **Set a Reminder** - Don't forget to check in every 48 hours
4. **Backup Your Secrets** - Store them in a password manager
5. **Tell Your Beneficiary** - Let them know this system exists

## 💡 Best Practices

- Use a strong, unique password for vault files
- Store the vault password in a password manager
- Include instructions INSIDE your vault files too
- Test the full process at least once
- Update check-in status regularly
- Keep beneficiary contact info current

## 📊 Cost Breakdown

| Service | Cost | Limit |
|---------|------|-------|
| GitHub Private Repo | **FREE** | Unlimited repos |
| GitHub Actions | **FREE** | 2,000 minutes/month |
| Gmail SMTP | **FREE** | 500 emails/day |
| 7-Zip | **FREE** | Open source |
| **TOTAL** | **$0/month** | ✅ |

## 🤝 Contributing

Found a bug? Have a suggestion? Open an issue or PR!

## 📄 License

MIT License - Feel free to use and modify

## ⭐ Show Your Support

If this helped you, give it a star! ⭐

---

**⚠️ DISCLAIMER:** This is a personal safety system. Test thoroughly before relying on it. The author is not responsible for any failures or issues. Always have multiple backup plans.

---

## 🙋 FAQ

**Q: Is this really free?**  
A: Yes! Uses GitHub's free tier.

**Q: Can GitHub see my files?**  
A: They're encrypted, so technically yes but they can't read them without your password.

**Q: What if GitHub shuts down?**  
A: Download your vault files locally as backup.

**Q: How secure is this?**  
A: AES-256 is "military-grade". Your biggest risk is password strength.

**Q: Can I use Outlook instead of Gmail?**  
A: Yes! Modify the SMTP settings in the workflow file.

**Q: What if I forget to check in?**  
A: Your beneficiary gets the email. Just check in again to reset the timer.

---

Made with ❤️ for peace of mind
