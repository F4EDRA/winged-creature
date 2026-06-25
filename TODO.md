# Winged Creature Launch TODO

Last checked: 2026-06-24

## Current State

- Live site: https://f4edra.github.io/winged-creature/
- GitHub repo: https://github.com/F4EDRA/winged-creature
- Local repo clone: `/Users/taralong/Documents/GitHub/winged-creature`
- Local webcam/filter prototype: `/Users/taralong/Desktop/flight-mode-filter/index.html`

The project currently has two separate pieces:

1. `winged-creature` is the public GitHub Pages website.
   - It loads successfully.
   - It is a simple artwork page with an embedded YouTube iframe.
   - The iframe still uses `PASTE_YOUTUBE_VIDEO_ID_HERE`, so the public page is not connected to a real stream yet.

2. `flight-mode-filter` is a local webcam filter.
   - It opens the local camera in the browser.
   - It mirrors the video feed.
   - It adds CSS-based wings, aura, scanlines, ring, and glitch overlays.
   - It does not stream anywhere by itself.
   - It should be captured by OBS, then OBS should stream to YouTube Live.

## Minimum Viable Plan For Tomorrow

The reliable path is:

1. Open the local filter in Chrome.
2. Capture that Chrome window in OBS.
3. Stream from OBS to YouTube Live.
4. Put the YouTube Live video ID into `winged-creature/index.html`.
5. Push the website update to GitHub.
6. Confirm the public page shows the live stream.

## Tonight: Must Finish

- [x] Confirm the filter runs locally:
  - Start server:
    ```sh
    cd /Users/taralong/Desktop/flight-mode-filter
    python3 -m http.server 8000
    ```
  - Open:
    ```text
    http://localhost:8000
    ```
  - In Chrome, allow camera access.
  - Confirm the camera appears and the wing/aura overlay is visible.

- [x] Install/open OBS and create a scene:
  - Source: Chrome window showing `http://localhost:8000`
  - Crop or fit the browser window so only the filter is visible.
  - Audio should be off unless the project explicitly needs audio.
  - Set output canvas to 1920x1080 if the presentation display supports it.
  - Confirm OBS preview shows the same wing filter that is visible in Chrome.

- [ ] Create/schedule the YouTube Live stream:
  - Open YouTube Studio.
  - Confirm live streaming is already enabled on the channel. YouTube says enabling a first encoder stream may take up to 24 hours, so this is the highest-risk item tonight.
  - Create a live stream for tomorrow.
  - Copy the stream key into OBS.
  - Copy the public YouTube video URL or video ID.

- [ ] Run a private/unlisted test stream tonight:
  - Start streaming from OBS.
  - Open the YouTube watch page in another browser/device.
  - Confirm the image is live and acceptable after YouTube's delay.
  - Confirm no audio is broadcasting if no audio is intended.

- [ ] Update the public website iframe:
  - Edit `/Users/taralong/Documents/GitHub/winged-creature/index.html`.
  - Replace:
    ```html
    https://www.youtube.com/embed/PASTE_YOUTUBE_VIDEO_ID_HERE
    ```
    with:
    ```html
    https://www.youtube.com/embed/YOUR_REAL_VIDEO_ID
    ```
  - Example: if the YouTube URL is `https://www.youtube.com/watch?v=abc123XYZ`, the embed URL is:
    ```html
    https://www.youtube.com/embed/abc123XYZ
    ```

- [ ] Commit and push the website change:
  ```sh
  cd /Users/taralong/Documents/GitHub/winged-creature
  git status
  git add index.html TODO.md
  git commit -m "Prepare live stream page"
  git push origin main
  ```

- [ ] Verify GitHub Pages after push:
  - Open https://f4edra.github.io/winged-creature/
  - Hard refresh the page.
  - Confirm the iframe is no longer blank/placeholder.
  - Confirm the embedded stream plays.

## Tomorrow: Arrival Checklist

- [ ] Bring laptop charger.
- [ ] Bring any HDMI/USB-C adapters needed for the presentation computer/projector.
- [ ] Confirm Wi-Fi access before setup time.
- [ ] Open Chrome to `http://localhost:8000` and allow camera.
- [ ] Open OBS and verify the scene is still pointed at the correct Chrome window.
- [ ] Start the local server again if needed:
  ```sh
  cd /Users/taralong/Desktop/flight-mode-filter
  python3 -m http.server 8000
  ```
- [ ] Start YouTube stream from OBS.
- [ ] Open the public page on another device and verify it shows the stream.
- [ ] Leave OBS, Chrome, and Terminal open during the presentation.
- [ ] Disable sleep/display sleep for the presentation window:
  - System Settings -> Battery/Power -> prevent sleep where possible.

## Risks To Control

- YouTube Live has delay. The public website will not be instant; expect latency.
- YouTube Live may not be available immediately on a channel that has never streamed before.
- GitHub Pages may take a short time to update after pushing.
- Browser camera permission can fail if the page is not loaded from `localhost` or HTTPS. `http://localhost:8000` is acceptable.
- OBS can lose a window capture if Chrome is closed/reopened. Re-check the OBS source before presenting.
- The deployed site currently cannot show anything real until the YouTube video ID is replaced.
- If YouTube blocks embedding for the stream, the fallback is to link directly to the YouTube watch page from the website.

## Fallback Plan

If the full website embed fails tomorrow:

1. Keep the local filter running in Chrome.
2. Use OBS/projector to display the filtered camera directly.
3. Put the YouTube watch link or a simple "Live feed" link on the public site.
4. Prioritize the presentation working in the room over perfect remote embedding.

## Nice To Have After The Basics Work

- [ ] Make the filter responsive for different camera aspect ratios.
- [ ] Add a visible "camera blocked" screen instead of a browser alert.
- [ ] Move the filter prototype into this repo under a clear folder, such as `filter/`.
- [ ] Add a short `README.md` runbook for future installs.
- [ ] Add a simple backup page with a direct YouTube link.
- [ ] Test on the actual presentation laptop and projector, not only the home setup.
