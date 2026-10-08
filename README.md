# Pincode Clubbing

Static web app for branch managers. Load the OMS "Page Selection Info" dump and get fully paid orders
grouped by pincode, ready to club onto one delivery agent.

## Rules applied
- Payment status = FULL_PAYMENT_DONE
- Order status in AGENT_TO_BE_ASSIGNED, DELIVERY_DATE_TO_BE_ASSIGNED, DELIVERY_PARTNER_ASSIGNED, OUT_FOR_DELIVERY
- Any branch
- Pincode = the 6 digits in the trailing "XXXXXX, INDIA" part of the address

## Files
- index.html – page
- assets/app.js – all logic (parsing, grouping, copy)
- assets/app.css – styles
- assets/vendor/xlsx.full.min.js – SheetJS 0.18.5 (Apache-2.0), self-hosted so no third-party CDN is contacted
- vercel.json – security headers, incl. a Content-Security-Policy that blocks all network calls from the page
- robots.txt – keeps the app out of search engines

## Privacy
- The dump is parsed in the browser tab. There is no server code, no API, no database.
- `connect-src 'none'` in the CSP means the browser itself refuses any fetch/XHR/beacon from the page,
  so data cannot be sent anywhere even by mistake.
- Nothing from the dump is written to localStorage, cookies or IndexedDB. The only saved value is the
  "copy IDs as" preference.
- No analytics, no external fonts, no CDN.
- Never commit dumps to the repo (.gitignore blocks .xlsx/.xls/.csv).

## Deploy
See the deployment steps shared with this project, or in short:
`npx vercel` (preview) then `npx vercel --prod` from this folder. Framework preset: Other. No build command.
