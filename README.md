# 🔐 Family Vault — Deployment Guide

A secure, encrypted PWA for storing family password hints and PINs.
Works on iPhones via Safari "Add to Home Screen" — no App Store needed.

---

## How It Works

- All hints are encrypted with **AES-256-GCM** before being saved
- Encryption uses **PBKDF2** (310,000 iterations) to derive keys from your passphrase
- Nothing is ever sent to a server — all data lives on the device
- To share the vault across family members, use **Export / Import** in Settings

---

## Deployment Options

### Option 1: GitHub Pages (Free, Recommended)

1. Create a free GitHub account at github.com
2. Create a new **public** repository (e.g. `family-vault`)
3. Upload `index.html` and `manifest.json` to the repository
4. Go to **Settings → Pages** and set Source to `main` branch
5. Your app will be live at `https://yourusername.github.io/family-vault/`
6. Share that URL with family members

**Add to iPhone Home Screen:**
- Open the URL in **Safari** (must be Safari, not Chrome)
- Tap the **Share** button (box with arrow)
- Tap **"Add to Home Screen"**
- Tap **"Add"** — it now behaves like a native app!

---

### Option 2: Netlify (Free, Drag & Drop)

1. Go to netlify.com and sign up free
2. Drag the `family-vault/` folder to their deploy drop zone
3. Get a URL like `https://your-name.netlify.app`
4. Optionally set a custom subdomain in Netlify settings

---

### Option 3: Self-hosted (Advanced)

Host on any static file server (Apache, Nginx, Caddy).
The app requires **HTTPS** for the Web Crypto API to work.

---

## Security Model

| Feature | Details |
|---|---|
| Encryption | AES-256-GCM |
| Key derivation | PBKDF2-SHA256, 310,000 iterations |
| Salt | Random 16 bytes per entry |
| IV | Random 12 bytes per entry |
| Storage | localStorage (device-only) |
| Network | None — fully offline after first load |

**What this protects against:**
- Someone finding/stealing the device and reading localStorage raw
- Server-side data breaches (there's no server)

**What it does NOT protect against:**
- Someone who already knows the family passphrase
- Malware on the device with localStorage access
- Someone watching over your shoulder when you type the passphrase

---

## Sharing Between Family Members

Since data is stored locally per device, family members sync via Export/Import:

1. **Person A** goes to Settings → Export Vault → copies the JSON
2. **Person A** sends the JSON to **Person B** via iMessage or AirDrop
3. **Person B** goes to Settings → Import Vault → pastes the JSON
4. Both people need the **same family passphrase** to decrypt

---

## Adding App Icons (Optional)

For a proper home screen icon:
1. Create a 192×192 PNG named `icon-192.png`
2. Create a 512×512 PNG named `icon-512.png`
3. Upload alongside `index.html`

Use an online favicon generator (e.g. realfavicongenerator.net) to create these.

---

## Future Features (Roadmap)

The app is built modularly to support:
- 🗺️ Vacation Planner
- 💬 Family Chat
- 🆘 Emergency Contacts
- 🔄 Cloud sync (iCloud, Dropbox)
- 👆 Face ID / Touch ID (Web Authentication API)

---

Built with React 18, Web Crypto API, and zero dependencies beyond CDN-loaded React.
