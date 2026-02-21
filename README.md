# obsidian-redirect

A lightweight GitHub Pages redirect that opens notes in [Obsidian](https://obsidian.md) from platforms that don't support custom URL schemes (e.g. Telegram).

## Why

Obsidian uses `obsidian://open?vault=X&file=Y` to open notes, but Telegram silently strips non-HTTPS links from messages. This page acts as an HTTPS intermediary: the link opens a hosted page that immediately redirects to the `obsidian://` URL.

## Usage

```
https://nikkosmo.github.io/obsidian-redirect/?vault=VAULT_NAME&file=NOTE_NAME
```

### Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `vault`   | Yes      | Obsidian vault name |
| `file`    | Yes      | Note filename (without `.md` extension) |

### Example

```
https://nikkosmo.github.io/obsidian-redirect/?vault=iCloud&file=Active%20Projects
```

Opens `Active Projects.md` in the `iCloud` vault.

## How it works

1. User taps an HTTPS link in Telegram (or any app)
2. Browser opens `index.html` on GitHub Pages
3. JavaScript reads `vault` and `file` query params
4. Page executes `window.location.href = 'obsidian://open?vault=...&file=...'`
5. OS handles the `obsidian://` protocol and opens Obsidian
6. If Obsidian doesn't open within 1.5s, a manual "tap here" fallback link appears

## Deployment

Hosted on GitHub Pages from the `main` branch. Any push to `main` triggers automatic deployment.

## Used by

- [Loom](https://github.com/NikKosmo/loom) -- Obsidian knowledge assistant with Telegram integration
