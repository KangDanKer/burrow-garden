# Burrow Garden

An unofficial companion for [Squeekchain](https://squeekchain.com). A small garden grows **only while the real hamster is running**. When the wheel idles, the hamster naps and nothing grows.

## How it uses live Squeekchain data
- Polls `https://api.squeekchain.com/v1/status` every ~1.5 s.
- **Spinning / active** and **RPM** drive growth: each reading adds `1 + RPM/30`.
- Each increase of `settledThroughRound` adds one "settlement seed".
- If readings stop for more than 6 s, a **reconnecting / stale-data banner** appears, growth pauses, and polling continues.
- Field names are matched case-insensitively (`state`/`status`/`spinning`, `rpm`/`speed`, `settledThroughRound`). Adjust `parse()` in `index.html` if the API shape differs.

## Design choices
- Single static file, no build step, no dependencies.
- Progress lives in `localStorage`; denied or corrupt storage falls back to memory.
- No prices, APY, or token balances are shown or fabricated.
- Respects `prefers-reduced-motion`.

## Run
Open `index.html`, or `npx serve .`

## Deploy to IPFS
Upload the folder (`index.html`, `cover.svg`) to a pinning service (Pinata, Storacha, Fleek) or run `ipfs add -r .`, then share the CID gateway link.

## License
MIT
