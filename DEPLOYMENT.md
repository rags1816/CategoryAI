# Deployment

**Individuals:** download `index.html`, open in Chrome/Edge. Everything runs locally; AI calls go only to the provider you configure (or use Sandbox — fully offline).
**Teams:** host the file on any static intranet/HTTPS location — same file, zero build. Each user's browser profile is an isolated workspace; shared PCs need separate OS logins or browser profiles. Distributing copies of the file is equally valid — isolation is automatic.
**Devices:** no sync by design. Hand off laptop↔mobile via ⬇/⬆ session .json (stamped; import replaces after confirm). One device at a time.
**Upgrades:** replace the file; data lives in the browser, not the file. Keep the sha256 (below) of what you deploy; the in-app 📜 Declarations and version footer identify builds.
**GitHub suggestion:** repo root = `index.html`, `README.md`, `USER_GUIDE.md`, `CHANGELOG.md`, `DEPLOYMENT.md`, `LICENSE`; enable GitHub Pages on the root and the app is live at your pages URL (still fully client-side).
