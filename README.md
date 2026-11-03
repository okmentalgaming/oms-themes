# oms-themes

Update channel for the OK Mental Production Suite. This repository holds only:

- `manifest.json` — what the app checks (`themes[]`, `themePacks[]`, `engine`, `app`)
- `ewc-<version>.zip` — theme packs (overlays are encrypted `.html.enc` files)
- `engine-<version>.pack`, `app-<version>.pack` — encrypted update packs (AES-256-GCM); only the app can open them
- `<theme>-<version>-<n>.pack` — a whole theme (overlays + media) as encrypted parts, listed in `themePacks[]` (app 1.0.8+)

Nothing here is readable without the application's key. Never reuse a pack file name — always bump the version.
