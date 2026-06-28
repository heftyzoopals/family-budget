# 💰 Family Budget

A shared budgeting app for two, built as a single HTML file. No installs, no subscriptions — just open the URL and track your money together in real time.

![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)

---

## Features

### Core
- **Shared in real time** — both partners see changes the moment they're made, powered by Firebase Realtime Database
- **Manual entries** — log income or expenses to any date, with name, amount, category, and who added it
- **Recurring entries** — set up repeating income or expenses with 8 frequency options; they auto-populate every matching date
- **Dark mode** — toggle light/dark independently on each device; preference is remembered per browser

### Calendar views
- **5 zoom levels** — Year, Quarter, Month, Week, and Day views; navigate with ‹ › or click to drill down
- **Year view** — 12-month grid with net totals and a proportional bar chart per month; click any month to zoom in
- **Quarter view** — 3-month side-by-side layout showing entries and net totals per month
- **Month view** — traditional calendar with color-coded entry pills per day
- **Week view** — 7-day strip with per-day projected balances and entry pills; click a day to expand details
- **Day view** — full timeline for a single day with a running balance updated after each entry

### Balance tracking
- **Account balance** — set your real bank balance any time; both partners see it instantly
- **Mid-day updates** — if you update the balance during the day, only entries added *after* that update are counted toward the daily total, keeping the number accurate no matter when you check
- **Daily balance** — every day shows its projected or actual balance; the banner shows "Balance as of 12:03 PM + entries since then" when anchored to a same-day snapshot
- **Projected end-of-month** — calculated from your current balance plus only the remaining entries in the month
- **Carry-forward balance** — month-end net automatically rolls into the next month's starting balance; browse past months and see accurate figures chained from your last update

### Recurring entry management
- **Edit a single occurrence** — override the name, amount, or category for one date without changing the rule (e.g. a higher paycheck or bigger electric bill); overridden instances show an "edited" badge
- **Reset to defaults** — remove an override and restore the recurring rule's original values
- **Skip one occurrence** — suppress a single date while keeping all future ones
- **Stop after a date** — set an end date on any recurring rule; future occurrences stop generating after that point
- **Delete all occurrences** — remove the rule entirely
- **Edit the rule** — change name, amount, frequency, category, or end date at any time; per-date overrides and skips are preserved

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
In Month view, click any day to open the detail panel, then tap **+ Add entry**. In Week or Day view, use the **+ Add entry** button directly. Fill in type (income or expense), name, amount, date, category, and optionally who added it.

### Zooming in and out
Use the **Year | Quarter | Month | Week | Day** bar above the calendar to change zoom level. The ‹ › navigation buttons step by the current zoom unit (one year, one quarter, one month, one week, or one day). Clicking a month cell in Year or Quarter view drills straight into that month.

### Recurring entries
Go to the **Recurring** tab to set up items that repeat automatically. They appear on every matching date across all months. On any recurring instance:
- **✎** — edit just that one occurrence (amount, name, category)
- **✕** — opens a choice: skip this date only, stop after a date, or delete all occurrences

### Updating your account balance
Tap **✎ Update balance** at the top of the app and enter the current balance from your bank. The app records the exact time of the update — any entries you add afterward are included in today's balance calculation; anything already reflected in your bank statement isn't double-counted.

### Carry-forward
When you navigate to a new month, the app automatically calculates your end-of-month balance and saves it as the starting balance for the next month. Browse forward or backward through months and the balance figures chain correctly from your last real update.

### Dark mode
Tap the 🌙 / ☀️ button in the top-right corner. Each device remembers its preference separately.

### Switching databases
Tap the ⚙ button in the header to disconnect and re-enter a different Firebase config.

---

## Firebase data structure

The app stores five top-level keys in your Realtime Database:

| Key | Contents |
|---|---|
| `entries` | One-time income and expense entries |
| `recurring` | Recurring rules, including `skippedDates`, `overrides`, and `endDate` per rule |
| `accountBalance` | `{ value, updatedAt, updatedBy }` — the latest balance snapshot |
| `monthlyBalances` | `{ 'YYYY-MM': number }` — carry-forward anchors per month |
| `balanceSnapshots` | `{ 'YYYY-MM-DD': { value, updatedAt } }` — intraday snapshots for accurate daily totals |

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

Your budget data lives in your own Firebase project — Anthropic, GitHub, and any third party have no access to it. The app is a static HTML file that communicates only with your Firebase database.

---

## License

MIT — do whatever you want with it.
