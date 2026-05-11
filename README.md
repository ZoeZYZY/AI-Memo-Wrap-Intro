# AI Memo Wrap

<p align="center">
  AI web clipper for saving webpage highlights as searchable notes with tags, categories, batch export, and optional Notion sync.
</p>

<p align="center">
  <a href="https://zoezyzy.github.io/AI-Memo-Wrap-Intro/">Home</a> ·
  <a href="https://zoezyzy.github.io/AI-Memo-Wrap-Intro/features.html">Features</a> ·
  <a href="https://zoezyzy.github.io/AI-Memo-Wrap-Intro/demo.html">H5 Demo</a> ·
  <a href="https://chromewebstore.google.com/detail/ai-memo-wrap/hlmadcmleiholmlengnlodmfobdbmdac">Install</a>
</p>

## Why AI Memo Wrap

- Highlight useful text on any webpage and save it with one click
- Build a searchable memo library with source links and timestamps
- Organize by categories, tags (`#tag` filters), and research sessions
- Batch copy, share rich digests, or export CSV
- Sync selected memos to Notion when needed
- Keep everything local by default, with optional cloud sync

## Visual Workflow

```mermaid
flowchart LR
  A[Highlight on webpage] --> B[Wrap with AI]
  B --> C[Add tags and categories]
  C --> D[Share memo or digest]
  D --> E[Sync to Notion]
```

## Feature Coverage

| Module | What it does |
|---|---|
| Flash Panel | Inline `Wrap ✨` capture from selected text |
| Side Panel | Memo list, filters, detail drawer, bulk actions |
| Memo Tags | Up to 10 tags per memo, max 24 chars each |
| Tag Filter | Search + `#tag` query + removable active chips |
| Categories & Sessions | Custom categories and session grouping for research workflows |
| Sharing | Copy / share memo, rich digest, subject, preview, body, and CTA output |
| Notion Sync | OAuth + cloud endpoint based sync |
| Cloud Sync (Optional) | Cross-device after login |
| Local-first Storage | Default `chrome.storage.local` mode |

## UI Component Preview

Open the visual component demo:

- [H5 Demo Page](./demo.html)

Demo contains:

- Flash capture widget
- Side panel memo cards
- Tag chips and filter bar
- Detail drawer preview
- Export/share action area

## Quick Start (Dev)

1. Install dependencies

```bash
npm install
```

2. Run UI preview

```bash
npm run dev
```

3. Build extension

```bash
npm run build:extension
```

4. Load unpacked extension

- Open `chrome://extensions`
- Enable `Developer mode`
- Click `Load unpacked`
- Select `dist-extension/`

## Tech Stack

- Chrome Extension Manifest V3
- React + TypeScript + Vite
- Tailwind CSS
- Supabase (Auth + Postgres + Edge Functions)
- Notion API

## Privacy & Security

- Local-first by default
- Cloud sync is opt-in
- Do not commit secrets
- Keep `.env.local` private
- Rotate tokens immediately if exposed

## Support

- Buy Me a Coffee: https://buymeacoffee.com/ZYZConsulting

## License

This project is currently **Proprietary / All Rights Reserved**.
See [LICENSE](./LICENSE).
