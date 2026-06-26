# 💰 Family Budget

A shared budgeting app for two, built as a single HTML file. No installs, no subscriptions — just open the URL and track your money together in real time.

![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)

---

## Features

- **Shared in real time** — both partners see changes the moment they're made, powered by Firebase Realtime Database
- **Calendar view** — browse income and expenses day by day with color-coded entry pills
- **Account balance tracking** — set your actual bank balance and see a projected end-of-month figure automatically
- **Day totals** — every day with transactions shows a live income / expense / net summary
- **Recurring entries** — set up repeating income or expenses (rent, paychecks, subscriptions) with 8 frequency options
- **Edit recurring entries** — update any recurring item in place without deleting and re-creating it
- **All entries list** — chronological view of the full month with per-day subtotals
- **Dark mode** — toggle light/dark independently on each device; preference is remembered
- **No account required** — connect once with your Firebase config and the app is ready

---

## Frequency options for recurring entries

| Option | Repeats |
|---|---|
| Every week | Weekly |
| Every 2 weeks | Biweekly |
| Every 3 weeks | Triweekly |
| Every month | Monthly |
| Every 2 months | Bimonthly |
| Every 3 months | Quarterly |
| Every 6 months | Semiannual |
| Every year | Annual |

---

## Setup

Full step-by-step instructions are in [SETUP.md](./SETUP.md). The short version:

1. **Create a free Firebase project** at [console.firebase.google.com](https://console.firebase.google.com)
2. **Enable Realtime Database** in test mode
3. **Copy your Firebase config** from Project Settings → Web app
4. **Enable GitHub Pages** in your repo settings (Settings → Pages → Deploy from branch → main)
5. **Open your GitHub Pages URL**, paste the Firebase config on first launch, and you're live

Your partner opens the same URL, enters the same Firebase config on their device, and you're both connected to the same data.

---

## Usage

### Adding an entry
Click any day on the calendar to open the day detail panel, then tap **+ Add entry**. Fill in the type (income or expense), name, amount, date, category, and optionally who added it.

### Recurring entries
Go to the **Recurring** tab to set up items that repeat automatically. They appear on every matching date across all months without any manual input. Use the ✎ button to edit an existing recurring entry, or ✕ to delete it.

### Updating your account balance
Tap **✎ Update balance** at the top of the app and enter the current balance from your bank. Both partners will see it immediately, and the app will calculate a projected end-of-month balance based on your entries.

### Dark mode
Tap the 🌙 / ☀️ button in the top-right corner. Each person's device remembers their preference separately.

### Switching databases
Tap the ⚙ button in the header to disconnect and enter a different Firebase config.

---

## Tech stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML, CSS, JavaScript (no framework) |
| Database | Firebase Realtime Database (free tier) |
| Hosting | GitHub Pages |
| Fonts | Inter via Google Fonts |

Everything runs in a single `index.html` file. No build step, no dependencies to install.

---

## File structure

```
family-budget/
├── index.html   # The entire app
├── README.md    # This file
└── SETUP.md     # Firebase + GitHub Pages setup guide
```

---

## Firebase free tier limits

Firebase's free Spark plan is more than enough for personal use:

- 1 GB stored data
- 10 GB/month download
- 100 simultaneous connections

A household budget with years of entries will use a tiny fraction of these limits.

---

## Privacy

Your budget data lives in your own Firebase project — Anthropic, GitHub, and any third party have no access to it. The app is a static HTML file; it communicates only with your Firebase database.

---

## License

MIT — do whatever you want with it.
