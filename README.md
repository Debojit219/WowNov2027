# WowNov2027

Wedding invitation site for Aratrik & Debojit. A single static page (`index.html`). On GitHub Pages it is served at
https://debojit219.github.io/WowNov2027/

## RSVP setup (Google Sheet, ~5 minutes)

1. Open the RSVP sheet: https://docs.google.com/spreadsheets/d/1AT_S2yqkLioWmDB-2KjbB4R_rvf8i_HwhOPMuhNNpTc/edit#gid=1875938154
   (Its ID and tab are already set in `rsvp-apps-script.gs`. Keep the sheet private, because it holds guest details.)
2. In the sheet, open **Extensions → Apps Script**. Delete the sample code and paste in the contents of `rsvp-apps-script.gs`.
   - `NOTIFY_EMAIL` is already set to both of our addresses. Each new RSVP is e-mailed to both of us.
3. Click **Deploy → New deployment**, choose type **Web app**, and set:
   - *Execute as*: **Me**
   - *Who has access*: **Anyone** (guests aren't signed in to Google; the script can only add rows and never returns sheet data)
4. Click **Deploy** and authorise. Copy the **Web app URL** (it ends in `/exec`).
5. In `index.html`, find `RSVP_CONFIG` and paste the URL:
   ```js
   const RSVP_CONFIG = {
       endpoint: 'https://script.google.com/macros/s/XXXX/exec',
       email: 'debojit.banerjee546@gmail.com,aratrikstudy@gmail.com'
   };
   ```
6. Send a test RSVP from the live site and check that a row appears in the linked tab of the sheet.

If you edit the script later, use **Deploy → Manage deployments → Edit → New version** so the URL stays the same.

Until `endpoint` is set, the form uses the `email` fallback: it opens the guest's mail app with the RSVP pre-filled and addressed to both of us.

## Link preview

The preview for WhatsApp, iMessage and similar apps uses `og-image.jpg` (1200×630) and the `og:*` tags in `index.html`. Those tags use absolute URLs.
If the site moves to a different address, update `og:url`, `og:image`, `twitter:image` and `canonical`.
WhatsApp caches previews, so a changed preview can take a while to show for links that were already shared.

## Assets

- Photos: `N.webp` (served to modern browsers) with `N.jpeg` as the fallback, both compressed.
- Music: `webmusic.m4a` (AAC, ~1.3 MB) is played first. `webmusic.mp3` is the fallback and is only downloaded by browsers that can't play AAC.
