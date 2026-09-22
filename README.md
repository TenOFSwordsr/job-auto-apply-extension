# Auto Job Apply - جاب اپلای خودکار

Manifest V3 browser extension that automatically submits applications on Iranian job
boards - Jobinja, Jobvision and E-Estekhdam. Written for Opera but is standard Chrome
extension code, so it loads in Chrome and Edge unchanged. Bilingual English/Persian UI.

**Suggested repo name:** `job-auto-apply-extension`
**Stack:** JavaScript, Chrome Extension Manifest V3 (`storage`, `activeTab`, `tabs`, `notifications`, `alarms`)
**Status:** incomplete
**Last modified:** 2026-07-22

## What it does

- `background/background.js` - service worker holding the message bus, application
  history, toolbar badge counter and desktop notifications. Seeds defaults
  (`enabled: true`) on `onInstalled`.
- `popup/popup.js` - 330-line control panel: enable/disable, per-board targeting and
  run history.
- Content scripts per board (`content/jobinja.js`, `content/jobvision.js`,
  `content/estekhdam.js`) are declared in `manifest.json` and are where the actual
  per-site apply automation would live.

## Layout

```
manifest.json          MV3 manifest, host permissions for all three boards
background/background.js
popup/popup.{html,js,css}
```

## Notes

- **The extension cannot run as-is.** `manifest.json` registers `content/common.js`,
  `content/jobinja.js`, `content/jobvision.js`, `content/estekhdam.js`,
  `styles/overlay.css` and `icons/icon{16,48,128}.png` - none of these exist in the
  folder. Loading it unpacked fails on the missing content scripts and icons.
  Only the background worker and popup were ever written.
- Automating applications may violate the boards' terms of service; treat this as
  personal-use tooling before publishing it publicly.
