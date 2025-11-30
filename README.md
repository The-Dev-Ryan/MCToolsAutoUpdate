# MeshCentralTools AutoUpdate  
Automatically trigger content updates in your MeshCentralTools content page whenever you publish a new GitHub Release.

## 📌 Overview  
MeshCentralTools AutoUpdate Content lets you keep your MeshCentralTools content, plugins, or tools automatically in sync with your GitHub repository.  
When enabled, MeshCentralTools provides an **HTTPS POST endpoint** and an **API key**.  
Your GitHub repository calls this endpoint whenever a **Release is published**, and MeshCentralTools pulls the latest content automatically.

---

## 🚀 How It Works  
1. MeshCentralTools provides:  
   - An **Auto Update Endpoint URL**  
   - An **API Key**  
   - A sample `curl` POST command  
2. GitHub Actions sends a POST request to this endpoint whenever a release is published.  
3. MeshCentralTools syncs the designated content item with your latest release.

---

## 🔐 Requirements  
From your MCTools Content Page (under **Auto Update**), gather:
- **Endpoint URL**
  
From your MCTools Dashboard Settings Page (under **API Key**), gather:
- **API Key**

---

## 🛠 Setup Instructions

### 1. Add Your API Key as a GitHub Secret  
Go to:

Settings → Secrets and variables → Actions → New repository secret

- Name: `MCTOOLS_API_KEY`  
- Value: *(Your MeshCentralTools API key)*

---

### 2. Create the GitHub Action Workflow  
Create this file:

`.github/workflows/mesh-autoupdate.yml`

Add the following:

```yaml
name: MeshCentral Auto Update

on:
  release:
    types: [published]

jobs:
  trigger_mesh_update:
    runs-on: ubuntu-latest
    steps:
      - name: Notify MeshCentral to Sync Content
        run: |
          curl -X POST "https://YOUR_ENDPOINT_URL_HERE"           -H "X-API-KEY: ${{ secrets.MCTOOLS_API_KEY }}"           -H "Content-Type: application/json"           --data '{ "ref": "main" }'
```

---

## ❓ Troubleshooting

### MeshCentral isn’t updating
- Confirm the API key is correct  
- Ensure the endpoint URL matches exactly  
- Check GitHub Actions logs  
- Confirm the slug matches the correct content entry  

### `403 Unauthorized` error
The API key is missing or incorrect. Re-add it in GitHub Secrets.

---

## 📄 License  
This documentation follows the licensing terms of the repository.
