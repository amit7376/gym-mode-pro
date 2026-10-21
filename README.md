# Gym Mode Pro — iPhone PWA (phone-only setup)

A static, offline-first workout tracker. Workout records are stored in IndexedDB in the browser on your iPhone. No Firebase, account, or cloud database is used.

## Features
- Muscle-group combinations and Full Body preset
- Exercise variations, weight, sets, reps, per-set completion and notes
- Start/pause/resume timer and session duration
- Local workout history and repeat workout
- Suggestions based on previous saved records
- JSON backup/restore and CSV export
- PWA manifest and service worker for offline app shell

## You can set this up using only your iPhone

A PWA must be served over HTTPS for reliable installation and service-worker/offline support. You do not need a computer, but you do need to publish these static files to a free HTTPS host once. Your workout data stays in the local IndexedDB database; this app does not upload workouts to the hosting provider.

### Option A: GitHub Pages using Safari on iPhone

1. Download `gym-mode-pro-pwa.zip` to your iPhone. In the Files app, open Downloads and tap the ZIP once to extract it. You should see a folder named `gym-mode-pro-pwa` containing `index.html`, `app.js`, `styles.css`, `manifest.json`, `sw.js`, `icon-192.png`, and `icon-512.png`.
2. In Safari, open `https://github.com` and sign in or create a free account.
3. Create a new **public** repository named `gym-mode-pro`. Do not initialize it with a README if you want to upload the included files as-is.
4. Open the new repository. Choose **Add file → Upload files**. In the iOS file picker, open the extracted `gym-mode-pro-pwa` folder and select the seven app files (`index.html`, `app.js`, `styles.css`, `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png`). Upload them to the repository root, not inside an extra nested folder. If the iPhone picker cannot select multiple files at once, upload them in several batches.
5. Commit the upload to the `main` branch.
6. In the repository, open **Settings → Pages**. Under build/deployment, choose **Deploy from a branch**, select `main` and `/(root)`, then Save.
7. Wait a minute or two and reopen **Settings → Pages**. Open the published HTTPS link shown there. It will look like `https://YOUR-USERNAME.github.io/gym-mode-pro/` (use the exact link GitHub provides; do not type a guessed username).
8. Open the published link in Safari. Tap **Share → Add to Home Screen**. If shown, enable **Open as Web App**, then tap **Add**.
9. Launch Gym Mode Pro from the new Home Screen icon. Create a test workout, mark a set complete, save it, close the app, and reopen it to confirm history remains.

### Important iPhone storage notes

- The app uses IndexedDB under the website's origin. Open the same published URL each time; changing domains or URLs to a different host can make the old records appear missing because each origin has its own database.
- Records are local to this iPhone/browser and do not sync to iCloud, Google Drive, or other devices.
- Do not clear Safari website data or remove the app/site data without exporting a backup first. Browser storage can be cleared or evicted by iOS in some circumstances.
- Export a JSON backup regularly in **Settings & backups** and save it to the iPhone Files app. To recover, use **Import JSON backup**. CSV is for viewing spreadsheet records; JSON is the restorable backup.
- The first online visit is needed to cache the app shell. After that, the service worker can serve the app offline, although some browser behaviors may vary.
- This is a PWA, not a native App Store app. It does not require Firebase or a paid database.

## Updating the app

When updating files, increment the cache version in `sw.js` (for example, `gym-mode-pro-v2`) so installed clients fetch the new assets. Existing IndexedDB records use database `GymModeProDB` and object store `workouts`; do not change the schema without a migration.

## Local data and privacy

The workout database is stored in IndexedDB in the browser. Hosting serves the app files only; workout entries are not sent to GitHub by this app. Export backups are created only when you request them. Keep backups in a safe location.
