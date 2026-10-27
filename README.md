# oms-themes

Update channel for the OK Mental Production Suite. This repository holds only:

- `manifest.json` — what the app checks (`themes[]`, `engine`, `app`)
- `ewc-<version>.zip` — theme packs (overlays are encrypted `.html.enc` files)
- `engine-<version>.pack`, `app-<version>.pack` — encrypted update packs (AES-256-GCM); only the app can open them

Nothing here is readable without the application's key. Never reuse a pack file name — always bump the version.
