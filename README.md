# Family Cycle Support – installable app package

This folder turns the single-file web app into an installable, offline-capable app (a PWA).
It contains no personal data. Your family's data is only ever saved inside each person's own browser.

## What is inside
| File | Purpose |
|---|---|
| `index.html` | The app itself (the latest version, empty, PIN required) |
| `manifest.webmanifest` | Tells phones the app's name, colors and icons |
| `sw.js` | Offline service worker (the app works without internet after the first visit) |
| `icons/` | App icons: 192, 512, maskable 512, iPhone icon, favicon |

Keep all files together, with `icons` as a sub-folder.

## Why host it yourself?
- **Your data survives updates.** On the claude.ai link every release started with empty storage. On your own stable address, updating `index.html` keeps everyone's data.
- **It becomes a real installable app** with an icon, full-screen mode and offline use.
- The app needs **HTTPS** (all hosts below provide it) for the PIN security and for installing.

---

## Option A: GitHub Pages (free, recommended)
GitHub Pages is free for **public** repositories (private repositories need a paid plan). The package has no personal data, so a public repository is fine. Use a less obvious repository name if you don't want the site easy to find.

1. Create a free account at github.com.
2. Click **+ → New repository**. Name it, for example, `family-care`. Choose **Public** and click **Create repository**.
3. Click **uploading an existing file** (or **Add file → Upload files**).
4. On a computer, drag in **everything inside this folder**: `index.html`, `manifest.webmanifest`, `sw.js` and the `icons` folder. Click **Commit changes**.
5. Open the repository **Settings → Pages**.
6. Under **Build and deployment → Source**, choose **Deploy from a branch**. Under **Branch**, choose `main` and `/ (root)`, then **Save**.
7. Wait up to about 10 minutes. Your app appears at `https://YOUR-USERNAME.github.io/family-care/`.

**To update later:** open the repository, upload the new `index.html` (and `sw.js` if it changed) over the old one, and commit. Also change `fcs-v1` to `fcs-v2` in `sw.js` so phones refresh their saved copy.

## Option B: Netlify (free, drag and drop)
1. Go to **app.netlify.com/drop** and drag this whole folder onto the page. You get a live link immediately.
2. **Important:** a site you don't claim is deleted after a short time (reported as about one hour). Click **Claim**, sign up for a free account and keep the site.
3. To update: open the site in Netlify, go to **Deploys**, and drag the updated folder there. The address stays the same.

Cloudflare Pages and Vercel also offer free static hosting with a similar upload flow. Free-plan limits change from time to time, so check the provider's current page before you commit to one.

---

## Install on the phones
**iPhone (Safari only):** open your address → tap **Share** → **Add to Home Screen** → **Add**.
**Android (Chrome):** open your address → menu **⋮** → **Install app** (or **Add to Home screen**).

The icon is labeled **Family Care**, a neutral name. To change it, edit `short_name` in `manifest.webmanifest` and `apple-mobile-web-app-title` in `index.html`.

### First-time setup on each phone
1. **Install first, then open the installed app.** On iPhone, the home-screen app has its own separate storage from Safari, so enter or restore data inside the installed app.
2. Create a PIN.
3. To bring your existing data: in your old version, go to **Settings → Backup → Export file**; in the new app, go to **Settings → Backup → Restore from a backup file**, review the preview and confirm.

## Troubleshooting
- **Asked to create a PIN every time you open the app?** The browser is not keeping the page's data. This happens on iPhone when the page is opened inside another app, or in Private Browsing. Open your hosted address in Safari, install it with **Add to Home Screen**, and use the installed icon. The app also shows a warning when it detects that saving is blocked.
- **Still seeing an old version after an update?** Close the app completely and open it twice, and make sure you bumped `fcs-v1` to `fcs-v2` in `sw.js`.

## Good to know
- **Offline:** after the first visit the app opens without internet. After you publish an update, phones show the new version the second time they open the app.
- **Data stays per device.** Each family member's phone has its own data and PIN. Nothing is uploaded anywhere.
- **Backups:** export regularly; clearing the browser's data or uninstalling the app erases the data.
- **Notifications:** reminders only appear while the app is open (a web app cannot send background alerts without a server).
- **Security:** the PIN is a privacy lock, not encryption. Backup files are readable text, so store them privately.
- **Your address is public** to anyone who knows it, but anyone opening it just sees an empty app with its own PIN setup.
- **Native stores:** to publish to the App Store or Google Play you would wrap this folder with a tool such as Capacitor and use a developer account (not included here).
