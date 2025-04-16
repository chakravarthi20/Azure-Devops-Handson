# 🔐 Azure Key Vault Integration with Azure DevOps (End-to-End Explanation)
## ✅ What is Azure Key Vault? 
Azure Key Vault is a cloud service that helps securely store and access secrets, encryption keys, and certificates. It is mainly used for:
- Secrets Management: Store tokens, passwords, certificates, API keys.
- Key Management: Encrypt and manage encryption keys.
- Certificate Management: Manage SSL/TLS certificates.

## 🧱 Step-by-Step Implementation
### 🧩 Step 1: Create Azure Key Vault 
Go to Azure Portal → Search and select Key Vaults → Click Create.
Choose your subscription, resource group, and set:
- Name: devopsks
- Region: East US
- Pricing Tier: Standard
- ✅ Soft delete: Enabled by default (retains deleted vaults for recovery)
- ⛔ Purge protection: Optional. If enabled, you can't delete the vault permanently until retention expires.
- 📝 Soft Delete helps recover your vault even if it’s deleted accidentally.
![image](https://github.com/user-attachments/assets/c581f737-6a8b-4e46-8ac5-2b0f82336439)

### 🔑 Step 2: Create a Secret in the Vault 
From Key Vault: Go to Secrets (left panel) → Generate/Import
Set:
Name: db-pass
Value: Your DB password
Optional: Set activation date and expiration if required
Click Create.
![image](https://github.com/user-attachments/assets/596f98fc-2b6e-4947-a537-de1c892cbd99)

## 🔄 Step 3: Connect Azure DevOps to Azure Key Vault
To securely use your secrets in Azure DevOps:
### 📌 3a. Set Access Policy (Refer Pic 4)
Go to Key Vault → Access policies → Create
- Select Secret permissions → Select All
- In next screen (Principal), search your Azure DevOps service connection name

🧭 How to get your Principal (Service Connection) Name:
- Go to portal.azure.com -> Search: Entra ID → Left panel: Enterprise Applications -> Find your Azure DevOps service connection name
- Copy and paste in the principal section → Select the correct entry → Click Create
![image](https://github.com/user-attachments/assets/90d54a3e-5591-449c-aed5-9208e5f91065)


### 🔗 Step 4: Link Key Vault in Azure DevOps Library 
Go to Azure DevOps → Library → New Variable Group
- Name: db password
- Enable: Link secrets from Azure Key Vault
- Choose: Azure subscription
- Key vault name: devopsks(In my case)
- Select the secret db-pass → Click Save
![image](https://github.com/user-attachments/assets/92ac3d70-1ada-467b-a749-b68686920882)

👉 This creates a secure reference to the secret that can be used in pipelines.

### 💡 Step 5: Use Secret in Pipeline
Go to your release pipeline or build pipeline
- Instead of writing the actual DB password, use: $(db-pass)
➡️ It pulls the value securely from Key Vault at runtime.
![image](https://github.com/user-attachments/assets/68ac44c9-354d-488f-9f8d-d993c144e455)

### ♻️ Step 6: Recover/Delete Key Vault (Refer Pic 7)
Even if your Key Vault is deleted:
- Go to Manage deleted vaults -> You’ll see your deleted keyvault devopsks
- Choose: 🔁 Recover to restore it
- ❌ Purge to delete permanently
![image](https://github.com/user-attachments/assets/9669b77e-fdc9-4ca4-8161-88d2b499474a)

## 🧾 Summary
- Created Azure Key Vault and securely stored db-pass as a secret.
- Gave Azure DevOps access using access policies by linking the service principal (found via Entra ID).
- Linked the secret in Azure DevOps library and securely used it in pipelines.

