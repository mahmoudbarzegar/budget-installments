# installments-pwa

**English** | [فارسی](README.fa.md)

An offline-first installment tracker PWA with full Persian (RTL) support. No backend, no build step. Your data stays on your device.

## Features

- Define multiple **sources** (wallet, loan, expenses, etc.), each with a name and a budget
- Add **installments** to each source with a title, amount, notes, and an optional **due date** (displayed in the Jalali calendar)
- Live totals per source: sum of installments, remaining budget, and a progress bar
- Two-screen layout: sources list, then the installments of a selected source
- Search installments and sort by creation order, nearest due date, or largest amount
- Mark installments as paid; overdue ones are highlighted in red
- Works offline after the first load
- Backup and restore via a JSON file
- Dark mode (follows the phone's system setting)

## Project structure

```
index.html     The entire app (HTML + CSS + JS)
manifest.json  PWA install metadata
sw.js          Service worker for offline support
icon.svg       App icon
```

There are no external dependencies and no build step.

## Install on your phone

A PWA needs **HTTPS** to be installable. The simplest option is GitHub Pages:

1. Put the four files above in the root of the repo.
2. Go to **Settings > Pages**, choose the `main` branch and the `/ (root)` folder.
3. After a minute or two the app is live at `https://USERNAME.github.io/installments-pwa/`.

(Alternative: drag the project folder onto `app.netlify.com/drop`.)

Then, on your phone:

- **Android (Chrome):** menu (⋮) > *Install app* or *Add to Home screen*
- **iPhone (Safari):** Share button > *Add to Home Screen*

## Run locally

Service workers don't work over `file://`, so start a local server:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

`localhost` is treated as a secure origin, so PWA install works there too.

## Data and backups

- All data is stored in the browser's `localStorage` on that device and is never sent to any server.
- Clearing site data or uninstalling the browser deletes it. Use the **Backup** button (bottom of the home screen) from time to time to export a JSON file.
- To move to another phone: export a backup, install the app on the new phone, and use **Restore**.

## Updating

After changing any file, bump the cache version in `sw.js` (for example `installments-v1` to `installments-v2`), commit, and push. Then close and reopen the app once to pick up the new version.

## Building an APK (optional)

If you want a native Android build, you can wrap this project with [Capacitor](https://capacitorjs.com):

```bash
npm init -y
npm i @capacitor/core @capacitor/cli @capacitor/android
npx cap init installments com.example.installments --web-dir=.
npx cap add android
npx cap open android
```

## License

MIT
