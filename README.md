# Imagicaa Navigator (unofficial PWA)

A mobile-first interactive guide built around Imagicaa's official illustrated Theme Park map.

## Included
- Tap-able map pins for attractions, food and facilities
- Attraction detail cards
- Search and category filters
- Live GPS marker projected onto the illustrated map after calibration
- Two-point GPS calibration: mark your real position at two recognisable places to estimate map scale and orientation
- Nearby list sorted by approximate map distance after GPS calibration
- Approximate walking route drawn over a hand-traced path network (verify against park signs)
- Ride completion checklist saved locally
- Next-stop suggestion based on approximate map proximity and incomplete rides
- PWA manifest and service worker for basic offline caching

## Important accuracy limitation
The official illustrated map is not a surveyed/georeferenced map and does not publish control-point coordinates or pedestrian path geometry. The app therefore uses a two-point calibration: at two recognisable places, tap your current position on the map while GPS is active. This estimates scale and orientation and projects subsequent GPS fixes onto the illustration. It is still approximate (illustrated maps distort distances); nearby distances are map estimates, not surveyed walking distances. Do not use it for emergency navigation; follow park signs and staff instructions.

The official map image is loaded from Imagicaa's public map URL on first load. For best offline reliability, open the app once while online and wait for the map to load.

## Deploy as an installable Android PWA
1. Upload the contents of this folder to a static HTTPS host (for example Netlify Drop, Cloudflare Pages or GitHub Pages).
2. Open the HTTPS URL in Chrome on Android.
3. Allow location permission when prompted.
4. At a recognisable spot, tap “Calibrate GPS” and mark where you are on the illustration. Repeat at a second recognisable place (for example, entrance then a clearly identified ride area) to improve alignment.
5. Use Chrome menu → Add to Home screen / Install app.
6. Open the app, wait for the map to load, then it can cache core assets for basic offline use.

## Notes
- Leaflet and the official park map are loaded from public CDNs / Imagicaa's website, so first load requires internet.
- Ride operation and wait times are not live-connected. Verify on the park's daily board.
- Attraction marker positions and map distances are approximate visual placements based on the published map.

## Deploy with GitHub Pages
1. Sign in to GitHub and create a new **public** repository named `imagicaa-navigator`.
2. Extract this ZIP on your computer or phone.
3. Open the repository, choose **Add file → Upload files**, and upload the *contents* of the `imagicaa-navigator` folder (so `index.html` is at the repository root, alongside `manifest.webmanifest`, `sw.js`, and `icon.svg`).
4. Commit the upload to the `main` branch.
5. Open **Settings → Pages**.
6. Under **Build and deployment**, choose **Deploy from a branch**; select branch `main` and folder `/(root)`, then Save.
7. Wait for GitHub Pages to publish. The URL will be `https://YOUR-GITHUB-USERNAME.github.io/imagicaa-navigator/`.
8. Open that HTTPS URL in Chrome on Android, allow location, then use the app's two-point calibration at two separated, recognisable outdoor locations. Add it to your Home screen from Chrome's menu.

Keep the repository public if using GitHub Free Pages. Do not upload secrets or personal data. GitHub Pages may take a few minutes to publish after the first save.


## Offline map build (v2)
The official park-map page supplied by the user is rasterized locally as `park-map.png` and displayed inside a native SVG viewport. Attraction pins, user marker and route overlays are drawn locally; the app no longer loads Leaflet or the map image from third-party servers. The service worker pre-caches `park-map.png` for offline use after the first successful visit. The park map itself remains an illustrated image; pins and walking paths are approximate, not surveyed.
