# CLAUSEAGE — Privacy Policy

Last updated: April 2026

CLAUSEAGE is a Chrome extension that displays your Claude AI usage limits as a compact floating widget on chat pages.

## Data Collection

CLAUSEAGE does **not** collect, transmit, store, or share any personal data. All processing occurs entirely within your browser.

## How It Works

The extension loads the Claude settings page (`claude.ai/settings/usage`) in a hidden, same-origin iframe within your existing browser tab. It reads the rendered usage data from the iframe's DOM and displays it in the floating widget. No data is sent to any external server.

## Local Storage

The only data stored locally (via `localStorage`) is the widget's screen position, so it remembers where you placed it. This data never leaves your browser and can be cleared at any time through your browser settings.

## Permissions

The extension requires no special Chrome permissions. It runs exclusively as a content script on `https://claude.ai/*` pages and does not access browsing history, cookies, tabs, or any other websites.

## Third-Party Services

None. The extension communicates only with `claude.ai`, which you are already logged into and using.

## Changes

Any changes to this policy will be reflected on this page with an updated date.

## Contact

If you have questions, contact [Nomad@88.com](mailto:nomad@88.com).
