# Squeek Watch

A live dashboard for [Squeekchain](https://squeekchain.com), the toy blockchain
whose blocks are mined by a real hamster running in a wheel.

**Live demo:** https://mercenary228.github.io/squeek-watch/

## What it shows

- **The wheel**: RPM, speed, distance run and work units from the hardware
  sensor, with an online/offline indicator (the wheel icon spins at the
  hamster's real pace).
- **Blocks**: block height, progress toward the next block, work per 1000
  blocks, the settlement queue and the last settlement transaction.
- **SQK supply**: SQK minted by the hamster versus the cap, current round,
  halving interval, total staked and live NFTs.
- **Latest on-chain activity**: the newest events from the Squeekchain
  indexer, each linked to its Sepolia transaction.
- **Contracts**: every Squeekchain contract address on Sepolia, linked to
  Etherscan.

## How it uses Squeekchain

It reads the public Squeekchain API straight from the browser:

| Endpoint | Used for |
|---|---|
| `GET /v1/status` | wheel sensor reading, block builder, settlement queue |
| `GET /v1/economy/state` | SQK supply, schedule, staking, NFTs, contract identities |
| `GET /v1/events?limit=12` | the activity feed |

It refreshes every 15 seconds, sends `If-None-Match` so unchanged data costs
nothing, and backs off on `429`/`5xx` using the API's `Retry-After`.

## Run it

It is one static file with no build step and no dependencies:

    open index.html          # or serve the folder with any static server

## License

MIT
