# UTOID Repository Map

This document lists the primary repositories that make up the UTOID system and
what each one contains. Use this as the entry point when navigating the code
and specifications.

## Core repositories

- **utoid**
  - System entry point and release-level documentation
  - Architecture overview, white paper, and FAQs

- **utocoin core** (currently hosted in `bitcoin`)
  - Chain implementation and consensus rules
  - UTXO ledger, PoW, and script extensions for promise arbitration
  - https://github.com/utoid/bitcoin

- **ipv7**
  - Transport layer implementation
  - Nodes, relays, SDK, and routing primitives
  - https://github.com/utoid/ipv7

- **utowallet**
  - Wallet daemon, CLI, SDK, and API specifications
  - Payment workflows: stake, cheque, promise, and sync
  - https://github.com/utoid/utowallet

## Supporting repositories

- **btcwallet**
  - External wallet component used for SPV in some setups
  - https://github.com/utoid/btcwallet

- **primitives**
  - Shared utilities and experiments
  - https://github.com/utoid/primitives

- **vpntest**
  - Internal testbed for relay and networking experiments
  - https://github.com/utoid/vpntest

## Documentation entry points

- UTOWallet docs: https://github.com/utoid/utowallet
- IPv7 overview: https://github.com/utoid/ipv7/blob/main/docs/OVERVIEW.md
- utocoin core: https://github.com/utoid/bitcoin
