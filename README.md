# Fixline — AI IT Support (clean, backend-free version)

This version has no custom backend and no server to run — it's plain HTML/CSS, and the
chat is Salesforce's own Embedded Messaging widget talking to your Agentforce agent
directly. GitHub Pages alone is enough to host this.

Files:
- `index.html` — the whole site
- `styles.css` — all styling

## 1. Add your Salesforce snippet

1. In Salesforce Setup, go to **Embedded Service Deployments** → your deployment.
2. Copy the **Code Snippet** shown there (starts with
   `window.embeddedservice_bootstrap = {...}` followed by a `<script src=...esw.min.js>`
   tag).
3. Open `index.html` in VS Code, find the comment near the bottom that says
   `PASTE YOUR SALESFORCE EMBEDDED MESSAGING SNIPPET BELOW THIS COMMENT`, and paste the
   snippet right after it, before `</body>`.
4. Save.

## 2. Preview it locally (optional)

Right-click `index.html` in VS Code → **Open with Live Server**. You should see the page
load, and Salesforce's chat bubble appear in the bottom-right corner after a few
seconds.

## 3. Push to your existing GitHub repo

To avoid the tangled git state from before, clone a fresh copy of your repo rather than
reusing the old folder:

```bash
cd Desktop
git clone https://github.com/chandininis21b-lang/fixline-site.git fixline-site-clean
```

Then:
1. Delete everything inside the new `fixline-site-clean` folder **except** the hidden
   `.git` folder (in VS Code Explorer, select all visible files/folders — `index.html`,
   `styles.css`, `script.js`, `README.md`, `backend`, whatever's there — and delete
   them. `.git` won't show in Explorer, so it's safe.)
2. Copy the two files from this clean version (`index.html`, `styles.css`) into that
   folder.
3. In the terminal, from inside `fixline-site-clean`:
   ```bash
   git add .
   git commit -m "Switch to Salesforce embedded widget, remove custom backend"
   git push
   ```
4. Give GitHub Pages a minute to rebuild, then open your live site and hard-refresh
   (Ctrl+F5).

## 4. Confirm your Embedded Service Deployment's Domain matches

In Salesforce Setup → Embedded Service Deployments → your deployment, make sure
**Domain** is set to your GitHub Pages URL (e.g. `https://chandininis21b-lang.github.io`).
If it doesn't match exactly, the widget won't load on your live site even though the
snippet is correct.
