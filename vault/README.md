# Place your encrypted .7z files here

Your encrypted vault files go in this folder.

## How to Create Encrypted Vault Files

### Windows:
```powershell
& "C:\Program Files\7-Zip\7z.exe" a -p"YOUR_PASSWORD" -mhe=on -mx=9 ".\vault\emergency-vault.7z" ".\your-files.txt"
```

### Mac/Linux:
```bash
7z a -p"YOUR_PASSWORD" -mhe=on -mx=9 "./vault/emergency-vault.7z" "./your-files.txt"
```

⚠️ **IMPORTANT:** Use the same password as your `VAULT_PASSWORD` GitHub secret!

## What Gets Included?

Include anything important that your beneficiary might need:
- Account passwords
- Important documents
- Contact information
- Instructions
- Legal documents
- Access codes
- etc.

## Example Files to Create

```bash
# Single emergency vault
7z a -p"PASSWORD" -mhe=on "./vault/emergency-vault.7z" "./important-docs/*"

# Separate vaults by category
7z a -p"PASSWORD" -mhe=on "./vault/financial.7z" "./financial-docs/*"
7z a -p"PASSWORD" -mhe=on "./vault/passwords.7z" "./passwords.txt"
7z a -p"PASSWORD" -mhe=on "./vault/legal.7z" "./legal-docs/*"
```

All vault files will be accessible to your beneficiary when the system triggers.
