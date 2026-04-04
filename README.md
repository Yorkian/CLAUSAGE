# CLAUSEAGE

A compact floating widget that displays your Claude AI usage limits in real time — right on your chat page.

No more switching tabs to check how much quota you have left.

![screenshot](screenshots/screenshot.png)

## What It Shows

- **Current session** — percentage used, progress bar, time until reset
- **Weekly limits** — percentage used, progress bar, next reset day
- **Plan badge** — your subscription tier displayed in the title bar (e.g. `CLAUSEAGE | Pro`)
- **Extra usage** — only appears when your Current balance is above $0
- **Live countdown** — "Updated: just now" → "half a minute ago" → ... → "Refreshing soon"

## Features

- 🎯 **Chat-only** — appears exclusively on `claude.ai/chat/*` pages, zero interference elsewhere
- 🔄 **Auto-refresh** — silently updates every 5 minutes; manual refresh anytime via the ↻ button
- 🖱️ **Draggable** — move it anywhere on screen, vertical position is remembered across sessions
- ➖ **Minimizable** — collapse to a tiny header bar when you need more space
- 🌙 **Dark mode** — adapts to your system theme and Claude's own dark mode
- 🔒 **Privacy-first** — no data leaves your browser, no external servers, no tracking, zero permissions

## How It Works

CLAUSEAGE injects a hidden same-origin iframe loading `claude.ai/settings/usage`, waits for React to render the usage data, parses the DOM, and displays the results in the floating widget. The iframe is destroyed immediately after extraction.

It also monkey-patches `history.pushState` / `replaceState` and listens for `popstate` to handle Claude's SPA navigation — so the widget correctly appears and disappears as you move between chat and non-chat pages.

If you're not logged in, the widget stays hidden.

## Install

### From source (Developer mode)

```bash
git clone https://github.com/Yorkian/CLAUSEAGE.git
```

1. Open `chrome://extensions`
2. Enable **Developer mode** (top right toggle)
3. Click **Load unpacked**
4. Select the cloned `CLAUSEAGE` directory
5. Open any `claude.ai/chat/` page — the widget appears in the bottom-right corner

### From Chrome Web Store

Coming soon.

## File Structure

```
CLAUSEAGE/
├── manifest.json      # Chrome extension manifest (Manifest V3)
├── content.js         # Core logic: iframe extraction, widget rendering, SPA navigation
├── content.css        # Widget styles with dark mode support
├── icon48.png         # Extension icon (48×48)
├── icon128.png        # Extension icon (128×128)
└── privacy-policy.html
```

## Technical Notes

- **Manifest V3** — no background service worker, no special permissions, content script only
- **Same-origin iframe** — since the widget runs on `claude.ai`, the iframe to `/settings/usage` is same-origin and accessible via `contentDocument`
- **DOM polling** — polls the iframe every 500ms (up to 20s) waiting for `"% used"` text to appear, indicating React has finished rendering
- **Position persistence** — vertical position saved to `localStorage`; horizontal position always snaps to the right edge on window resize
- **Auto-refresh timer** — `setInterval` at 5 minutes; resets on manual refresh to avoid double-fetching

## Compatibility

- Chrome / Chromium-based browsers (Edge, Brave, Arc, etc.)
- Manifest V3
- Requires an active `claude.ai` session

## Privacy

CLAUSEAGE does **not** collect, transmit, or store any personal data. All processing happens locally in your browser. The only data stored is the widget's screen position via `localStorage`.

[Full privacy policy](privacy-policy.html)

## License

MIT

## Author

**York** — [@Yorkian](https://github.com/Yorkian)
