# Dropzone — Secure File Sharing Design Demo

A browser prototype for the sharing flow: file selection, expiry choices, generated opaque demo tokens, a local activity list, and revoke controls.

## Run

Open `index.html` in a modern browser. No build step or server is needed.

## Important security boundary

This is a UI and threat-modeling exercise only. It does not upload, encrypt, or share file contents. The selected file remains in the page, and link tokens are local demo records in browser storage. Do not use real, personal, or sensitive files. The project must not be presented as a production secure-sharing service.

## Production design notes

- Keep file bytes in private object storage and serve only through an authorization service.
- Generate high-entropy, single-purpose tokens; store only a hash of each token server-side.
- Enforce expiry, revocation, download limits, and authorization on the server for every request.
- Encrypt in transit and at rest; use managed keys and a documented rotation plan.
- Validate file size and type, scan uploads, and use safe download headers.
- Rate-limit token checks; avoid logging raw tokens or sensitive filenames.
- Add audit events, abuse controls, retention/deletion jobs, and security tests.

## Threat model

Assets: file contents, share-token capability, recipient access, and audit metadata. Threats include token guessing or leakage, unauthorized downloads, malicious uploads, overlong retention, and access after revocation. The browser mock does not mitigate those threats; it exists to demonstrate the user flow and make the production requirements visible.
