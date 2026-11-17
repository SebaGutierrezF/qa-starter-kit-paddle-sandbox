# QA Automation Starter Kit — Paddle Sandbox landing

This is a **sandbox-only test storefront** based on the seller's existing Gumroad design. It includes no private ZIP and does not deliver any files.

## Files

- `index.html`: responsive single-file landing + official Paddle.js v2 from CDN; **test_** client-side token, **pri_** Sandbox price ID, three gated checkout buttons; clear TEST MODE disclosure.
- `.nojekyll`: allow direct static publishing to GitHub Pages.

## Local preview (no checkout verification)

Run `python -m http.server 8766` in this folder, then open http://127.0.0.1:8766/. The page requires internet access to load the official Paddle.js CDN.

## Publish as a separate public GitHub Pages site

1. Create a new *public* GitHub repository, suggested name: `qa-starter-kit-paddle-sandbox`. **Do not upload the commercial ZIP, API keys, passwords or source code.**
2. Upload only `index.html` and `.nojekyll` from this folder to the repository root.
3. In GitHub > repository Settings > Pages, choose Deploy from a branch > `main` > `/(root)` and Save.
4. Wait for Pages to display the actual HTTPS address. It will look like `https://USERNAME.github.io/REPO/`; do not invent it in Paddle.
5. Open the public site and check the ribbon says `PADDLE SANDBOX` and no real payments are possible.
6. Paddle **Sandbox** > Checkout > Checkout configuration > Default payment link: paste the actual published HTTPS Pages URL and save. Sandboxes do not require live domain approval. The link must be a real page with Paddle.js; don't use the Gumroad storefront URL.
7. Open the GitHub Pages site, click `Test checkout` and confirm Paddle's test checkout shows the Pro product at base US$49 and quantity 1. For testing only, Paddle docs list card `4242 4242 4242 4242`, any future expiry date, CVC `100`.
8. Confirm the test transaction is recorded in **Paddle Sandbox > Transactions**. The page explicitly warns that it **does not deliver the product ZIP**.

## Critical limitations / live prerequisites

- The token with `test_` and `pri_` price belong only to the Sandbox workspace; they are not live credentials.
- Never put secret Paddle API keys, webhook secrets or the private Pro ZIP in this public repository.
- No server-side fulfillment is implemented yet. A browser `checkout.completed` callback **must never grant ZIP access**. The future service must verify webhook signatures, idempotency, transaction item/price and payment status, then issue short-lived download links.
- A Paddle Live website requires domain approval, customer-facing product pages, real terms/privacy/refund/contact information, a separate live client token and a separate live Price ID.
- The staging page includes an optional link to the already-working live Gumroad listing.
- Current displayed `$49` is a base USD price; buyer-specific currency conversion/tax may vary at checkout.
- This site is a **candidate**, not yet validated against Paddle servers or checkout; verify the hosted checkout end-to-end.

Official docs:
https://developer.paddle.com/paddle-js/about/
https://developer.paddle.com/build/transactions/default-payment-link/
https://developer.paddle.com/get-started/quickstart/
