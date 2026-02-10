# UTOID

UTOID is an identity-first system that unifies anonymous transport, off-chain
payments, and on-chain settlement. It is designed to make private routing,
real-time value exchange, and on-chain arbitration work together as one stack.

The system is composed of three cooperating layers:

- **IPv7**: an anonymous, multi-hop transport network addressed by A7.
- **utocoin**: a UTXO settlement chain with stake-backed promises.
- **UTOWallet**: wallet daemon, CLI, and SDK that manage identity, off-chain
  state, and SPV chain connectivity.

## System status

- Network stage: testnet
- Consensus: scrypt PoW, 1-minute blocks
- Wallet-chain integration: SPV between UTOWallet and the chain

This repository is the entry point for UTOID and provides release-level
architecture, documentation, and cross-repo navigation.

## Design principles

- **Identity-first**: one canonical identifier format across transport and
  payments.
- **Privacy by default**: multi-hop routing and end-to-end encryption.
- **Off-chain speed, on-chain finality**: promises for low latency, chain
  arbitration for disputes.
- **Open integration**: APIs and SDKs for Web2 and Web5 workflows.

## Architecture at a glance

```
+--------------------+        +---------------------+        +------------------+
| Applications       | <----> | UTOWallet           | <----> | IPv7             |
| Web / Mobile / API |        | walletd / CLI / SDK |        | Route / Relay    |
+--------------------+        +----------+----------+        +--------+---------+
                                        |                           |
                                        | SPV / RPC                 | Multi-hop
                                        v                           v
                                  +-----------+               +------------+
                                  | utocoin   |               | IPv7 Mesh  |
                                  | chain     |               | relays     |
                                  +-----------+               +------------+
```

## Core concepts

- **UTOID**: the system-wide identity format.
- **A7**: the same format used specifically as the IPv7 network address.
- **Stake**: on-chain collateral locked for a defined period.
- **Cheque**: on-chain UTXO used as a payment unit.
- **Promise**: signed off-chain commitment that references stake and cheque
  proofs.

## Repositories

- **utocoin core** (currently hosted in `bitcoin`): chain implementation and
  consensus rules. https://github.com/utoid/bitcoin
- **ipv7**: network node, SDK, and relay components.
  https://github.com/utoid/ipv7
- **utowallet**: wallet daemon, CLI, SDK, and API specs.
  https://github.com/utoid/utowallet
- **btcwallet**: external wallet component used for SPV in some setups.
  https://github.com/utoid/btcwallet
- **primitives**: shared utilities and experiments.
  https://github.com/utoid/primitives
- **vpntest**: internal testbed for relay and network experiments.
  https://github.com/utoid/vpntest

## Documentation

- [How It Works](HOW_IT_WORKS.md)
- [FAQ](FAQ.md)
- [White Paper](WHITE_PAPER.md)
- [Repository Map](docs/REPOSITORIES.md)
- [Glossary](docs/GLOSSARY.md)
- [Contributing](CONTRIBUTING.md)
- [Security](SECURITY.md)
- [Code of Conduct](CODE_OF_CONDUCT.md)

### Component docs

- UTOWallet README: https://github.com/utoid/utowallet#readme
- UTOWallet Consensus: https://github.com/utoid/utowallet/blob/main/CONSENSUS.md
- UTOWallet Usage: https://github.com/utoid/utowallet/blob/main/USAGE.md
- IPv7 Overview: https://github.com/utoid/ipv7/blob/main/docs/OVERVIEW.md

## Getting started for developers

1. Read the system overview in [HOW_IT_WORKS.md](HOW_IT_WORKS.md).
2. Follow UTOWallet usage and consensus docs for wallet flows.
3. Integrate IPv7 if you need anonymous transport or relay services.

## License

MIT. See [LICENSE](LICENSE).
