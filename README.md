# AI Memo Wrap

AI-native Chrome extension for capturing highlights from any webpage, organizing them as memos/tasks, and syncing to Notion.

## Highlights

- Flash Panel on text selection (`Wrap ✨`)
- Side Panel workflow (memo list, filters, bulk export)
- Category system (custom category, color, icon, defaults)
- Tag system
  - Up to 10 tags per memo
  - Up to 24 characters per tag
  - Search + `#tag` filtering
  - Removable active filter chips (`x`) for recovery from mis-click
- Memo detail drawer (full content view, prev/next, copy/share/sync)
- Notion sync (OAuth + server-side edge functions)
- Optional Supabase Cloud Sync (cross-browser / cross-device after login)
- Local-first storage by default (`chrome.storage.local`)

## Tech Stack

- Chrome Extension Manifest V3
- React + TypeScript + Vite
- Tailwind CSS
- Supabase (Auth + Postgres + Edge Functions)
- Notion API

## Project Structure

```text
src/
  background/          # service worker entry
  content.ts           # page selection / flash panel injection
  sidepanel/           # side panel app entry
  components/          # UI components
  notionCloud.ts       # notion cloud sync client calls
  cloudSync.ts         # supabase cloud sync client calls
public/
  manifest.json        # dev manifest source
scripts/
  build-extension.mjs  # extension build + stable key manifest output
```

## Local Development

1. Install dependencies

```bash
npm install
```

2. Run web preview (UI only)

```bash
npm run dev
```

3. Build Chrome extension package

```bash
npm run build:extension
```

4. Load extension in browser

- Open `chrome://extensions`
- Enable **Developer mode**
- Click **Load unpacked**
- Select `dist-extension/`

## Environment Variables

Do not commit real keys/tokens.  
Use `.env.local` (gitignored) for local secrets.

Create from template:

```bash
cp .env.example .env.local
```

Required for Cloud Sync:

- `VITE_SUPABASE_URL`
- `VITE_SUPABASE_ANON_KEY`
- `VITE_AUTH_REDIRECT_TO`

Required for Notion:

- `NOTION_CLIENT_ID`
- `NOTION_CLIENT_SECRET`
- `NOTION_REDIRECT_URI`
- `NOTION_DATA_SOURCE_ID`

Optional fallback names still supported:

- `VITE_NOTION_CLIENT_ID`
- `VITE_NOTION_CLIENT_SECRET`
- `VITE_NOTION_REDIRECT_URI`
- `VITE_NOTION_DATA_SOURCE_ID`

## Storage Model

- Default mode: Local only (`chrome.storage.local`)
- Optional mode: Supabase Cloud Sync (account-based)
- Free-tier quota per account:
  - Max memos: `2000`
  - Max cloud size: `3 MB`

If quota is exceeded, cloud sync is blocked and a warning is shown.

## Privacy & Security

- Local-first by default (no forced account)
- Cloud Sync is opt-in
- Do not store secrets in source files
- Keep `.env.local` private
- Rotate tokens immediately if exposed
- Verify Notion DB is shared only with intended integration
- See [SECURITY.md](./SECURITY.md) for incident response and key rotation checklist

## Notion Setup (Production Path)

1. Create a **Public Notion integration** (OAuth enabled).
2. Add redirect URI:
   - `https://<your-extension-id>.chromiumapp.org/`
3. Set related secrets in Supabase Edge Functions and `.env.local`.
4. Connect in extension Settings -> Integrations -> Notion.
5. Confirm your Notion database/data source is connected and writable.

## Supabase Setup (Cloud Sync)

1. Enable Email auth (OTP / Magic Link based on your policy).
2. Create tables + RLS (project SQL scripts).
3. Deploy required edge functions (Notion OAuth + sync endpoints).
4. Fill `.env.local` and rebuild extension.

## Troubleshooting

- Flash bubble not showing:
  - Ensure extension is enabled
  - Refresh target page after extension update
  - Check `Settings -> Show Flash Panel`
  - Some embedded/sandboxed frames may block injection
- Notion sync failed:
  - Re-check `NOTION_DATA_SOURCE_ID`
  - Reconnect Notion OAuth
  - Verify database is shared with the correct integration
  - Check Supabase Edge Function logs
- Cloud sign-in says `Email not confirmed`:
  - Confirm inbox link using production redirect URL, not localhost

## Support

- Buy Me a Coffee: https://buymeacoffee.com/ZYZConsulting

## License

This project is currently **Proprietary / All Rights Reserved**.  
See [LICENSE](./LICENSE).
