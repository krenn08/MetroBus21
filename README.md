# MetroBus21
# Bus 21 — Next Bus to Métro Longueuil

A tiny, no-frills web app that shows Esther the next RTL **bus 21** departures from her stop, at a glance. Tap the icon, see when the bus comes. No login, no app store, no typing.

- **Stop:** Grande Allée / Édouard
- **Direction:** Terminus Longueuil (Métro Longueuil–Université-de-Sherbrooke), ~10 min ride
- **Shows:** the bus that just left, the next bus (big), and the 3 after that
- **Knows the day:** picks the right Weekday / Saturday / Sunday schedule automatically from the phone's clock

## What it looks like

A green card up top with the **next bus** time and a "in X min" countdown (it turns orange when the bus is 5 minutes out or less). Below it, "just left" and the following three departures. It refreshes itself every few seconds — nothing to press.

## How it works

Everything runs on the phone. All the scheduled times are built into the page (in `index.html`), and the app just compares them to the current time. That means:

- **No internet needed to calculate times** — it uses the phone's own clock.
- **No accounts, no tracking, no data collection.**
- It correctly handles after-midnight buses (e.g. Friday's 12:19 AM trip actually runs early Saturday), by checking yesterday / today / tomorrow's service.

> Note: it assumes the phone is set to Montreal/Eastern time (it always is, for a phone used here).

## Install on an iPhone (one time, ~30 seconds)

1. Open the app's web link in **Safari** (must be Safari, not Chrome — that's what makes it full-screen).
2. Tap the **Share** button (square with an up-arrow, at the bottom).
3. Scroll down and tap **Add to Home Screen**, then **Add**.
4. A green **Bus 21** icon appears. Tapping it opens the app full-screen, like any other app.

## Hosting (for whoever sets it up)

The app is a single file, `index.html`. Put it anywhere that serves a web page:

**Netlify Drop (easiest):**
1. Go to `app.netlify.com/drop` and sign in (free — the Google button is quickest).
2. Drag the whole `bus21-app` folder onto the page.
3. It publishes and gives a link like `https://your-name.netlify.app`.
4. Optional: **Site configuration → Change site name** to something memorable, e.g. `esther-bus21`.

Any static host works too (GitHub Pages, your own web space, etc.). The file must be reachable at a URL for the Home Screen icon to work.

## Updating the schedule

RTL changes its schedules a few times a year (seasonal). When that happens:

1. Get the fresh times for stop **Grande Allée / Édouard**, direction Terminus Longueuil.
2. Replace the three lists (`week`, `sat`, `sun`) inside the `SCHED` block near the bottom of `index.html`. Values are **minutes after midnight** of the service day; a value over 1440 means after midnight (e.g. `1459` = 12:19 AM the next day).
3. Re-upload / re-drag the folder to the **same** host. The link and the Home Screen icon stay the same — only the times change.

**Data source:** TransSee stop schedule for `rtl.21.1854`
(`https://www.transsee.ca/stopsched?s=rtl.21.1854`). Times in this version were pulled in **August 2026** (summer schedule).

## Files

- `index.html` — the app (this is the one you host)
- `README.md` — this file

## Nice-to-haves (not built yet)

- **Full offline caching** so it opens even with zero signal at the stop.
- **Automatic monthly check** that re-pulls the stop and flags any RTL schedule change.
