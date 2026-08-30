# Office Attendance Ledger — standalone app (no login)

Plain HTML/CSS/JS, no build step, no framework, no backend. All data is stored
in the browser (`localStorage`) on whichever device opens the page.

Files:
- `index.html` — the whole app: tracker + quarterly report
- `style.css` — styling
- `holidays.js` — admin-controlled company holiday list (see below)

## Setting company holidays (admin-only, since there's no login)

Open `holidays.js` and add entries like:
```js
const COMPANY_HOLIDAYS = {
  '2026-01-01': "New Year's Day",
  '2026-08-15': "Independence Day",
};
```
Then redeploy (re-drag the folder to Netlify, or re-push if using Git-based
hosting). Every date listed here shows up on everyone's calendar marked 🔒
and defaults to "Holiday" — it's excluded from working-day counts
automatically. Each person can still tap that date and pick a different
status just for themselves (e.g. they actually came in, or took PTO that
day) — the holiday is a default, not a hard lock, and clearing the override
restores the holiday. There is no button or screen inside the app for
entering the holiday list itself, on purpose — since the app has no
accounts, "admin" here just means "whoever controls this file and the
deployment," not a role inside the running app.

## What this means in practice

- **No sign-in required.** Open the page and start logging days.
- **Data lives only on that browser/device.** If you open the same URL on
  your phone and your laptop, they'll have two separate, unconnected sets
  of data — there's no syncing between them.
- **Clearing browser data (cache/cookies/site data) erases it, with no
  recovery.** Use the **"Export backup"** button any time to download a
  JSON file with everything logged so far. There's no import button wired
  up in the UI yet — say the word if you want one added back in.
- **Sharing the URL with others** gives each person their own independent
  copy of the app with their own local data — nothing is shared or visible
  between people, since there's no server or database behind it.

## Deploy it

Any static host works, no configuration needed since there's no backend to
connect:

1. Go to https://app.netlify.com/drop
2. Drag the `attendance-app` folder onto the page.
3. You get a live URL instantly, e.g. `https://your-app.netlify.app`.

Alternatives: GitHub Pages, Vercel, Cloudflare Pages — all free, all just
need these two static files.

## If you want real accounts + a shared database back

The previous version of this app (with email/password + Google sign-in and
a real Postgres database via Supabase, so data synced across devices and
each person's entries stayed private and recoverable) is available if you
want to switch back — just ask.
