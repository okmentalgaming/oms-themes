# OK Mental Production Suite — OTA theme/overlay updates

This public repo is the **Updates source** the app pulls from. In the app:
**Settings → Updates source (admin) → GitHub repository** = `okmentalgaming/oms-themes`.

## How the app checks for updates
1. It fetches `https://raw.githubusercontent.com/okmentalgaming/oms-themes/main/manifest.json`.
2. For each theme in `manifest.json`, it compares `version` to the version installed
   on that PC (the theme's `theme.json`). **Any difference = an available update.**
3. Updates are filtered by the signed-in client's **allowed themes** entitlement, then
   the theme's `url` (a `.zip`) is downloaded and **extracted over** the theme folder.
   Extraction overwrites changed files and leaves everything else in place — so update
   packs can be **incremental** (ship only the files that changed).

## manifest.json format
```json
{
  "themes": [
    { "id": "ewc", "name": "EWC", "version": "1.0.1",
      "url": "https://github.com/okmentalgaming/oms-themes/releases/download/ewc-1.0.1/ewc-1.0.1.zip" }
  ]
}
```

## To push an overlay update
1. Edit the overlay HTML, then **encrypt** it to `<name>.html.enc` (AES-256-GCM, app key).
2. Put the changed `.enc`/asset files (and a `theme.json` with the new version) in a ZIP,
   with files at the ZIP **root** (e.g. `Index.html.enc`, `theme.json`).
3. Upload the ZIP (GitHub Release asset for large packs; raw file for small ones).
4. Bump that theme's `version` + `url` in `manifest.json`, commit.
5. Clients click **Updates → Check for updates** and the pack installs with no reinstall.

Large binary assets (HD maps, video, audio) ship inside the installer bundle; OTA packs
should carry only what actually changed.
