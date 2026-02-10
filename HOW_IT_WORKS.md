# How UTOID Works

UTOID combines an anonymous transport network (IPv7), a settlement chain
(utocoin), and a wallet layer (UTOWallet). The system separates identity,
transport, and settlement while keeping them interoperable end to end. This
document provides a product-level explanation aligned with the current
implementation.

## 1. System overview

UTOID consists of:

- **Identity layer**: a single identifier format used across the stack.
- **Transport layer (IPv7)**: anonymous multi-hop routing addressed by A7.
- **Settlement layer (utocoin)**: UTXO chain used for collateral and dispute
  resolution.
- **Wallet layer (UTOWallet)**: manages keys, off-chain state, and SPV chain
  connectivity.

High-level interaction:

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

## 2. Identity and addressing

- **UTOID** is the canonical identifier format for the system.
- **A7** is the same format used specifically as the IPv7 network address.

The wallet keeps payment addresses (UTXO addresses on utocoin) separate from
network addressing, while allowing applications to use a single identity
primitive across layers. This separation reduces cross-layer leakage while
keeping user experience consistent.

## 3. IPv7 transport model

IPv7 provides anonymous, multi-hop routing without a global registry. Each
node maintains a limited set of neighbors. Routing is discovered on demand and
optimized by cost, latency, or privacy preference.

Core steps:

1. **Route discovery**: clients request candidate paths to a target A7.
2. **Handshake**: encrypted sessions are established between endpoints.
3. **Sync**: small control and state messages are exchanged over the session.
4. **Transmission**: application payloads flow as encrypted frames.

Routing remains private because each hop only sees its adjacent peers. Pricing
can be applied per hop and settled by the wallet layer.

## 4. Wallet and chain integration

UTOWallet is the user-facing system entry point. It performs:

- Key management for A7 and payment keys.
- Off-chain state management for promises, cheques, and stakes.
- SPV connectivity to the chain for confirmations and proofs.
- Authenticated APIs and peer-to-peer synchronization.

The wallet daemon (walletd) exposes HTTP and IPv7 APIs. The CLI and SDK are
thin clients that sign requests and submit them to walletd. Consensus behavior
and API contracts are defined in the UTOWallet repository.

## 5. Off-chain payments: stake, cheque, promise

UTOID uses stake-backed promises to enable low-latency payments while
preserving on-chain finality.

### 5.1 Objects

- **Stake**: on-chain collateral locked for a defined period.
- **Cheque**: on-chain UTXO used as a spendable payment unit.
- **Promise**: signed off-chain commitment referencing stake and cheque proofs.

### 5.2 Flow

```
Payer:  create stake -> create cheque -> issue promise
Payee:  verify promise -> accept updates -> commit or burn on chain
```

- The payer can update the promised amount off chain.
- The payee keeps the highest valid promise state.
- If settlement or arbitration is required, the payee commits on chain or
  triggers a burn path under the promise rules.

### 5.3 Stake and cheque lifecycle

```
Stake
+-----------+   lock on chain   +-----------+   used off chain   +-----------+
| Created   | ----------------> | Active    | <----------------> | In-Use     |
+-----------+                   +-----------+                    +-----------+
        |                                                        |
        | redeem or expire                                       | burn
        v                                                        v
+-----------+                                              +-----------+
| Redeemed  |                                              | Burned    |
+-----------+                                              +-----------+
```

Cheques follow a similar lifecycle: created on chain, reserved by the wallet,
then committed or released depending on outcome.

## 6. Peer synchronization

Wallets remain aligned using a peer-to-peer sync protocol. Each side exchanges
updates for the current promise state, expected amount, and commit status. This
ensures both parties converge on the same transaction view without requiring a
central coordinator.

## 7. API surface and authentication

UTOWallet exposes authenticated HTTP and IPv7 APIs. Requests are signed by the
caller and include wallet identity headers. This prevents unauthenticated
access and allows peers to verify intent and provenance.

The API surface includes:

- Transaction creation and updates (payer and payee flows)
- Stake and cheque lifecycle operations
- Peer synchronization and status
- Chain delegations via the wallet daemon

## 8. Cost and settlement model

IPv7 relays can quote fees per hop. The wallet layer can select routes based on
cost, latency, or privacy. When payments are enabled, utocoin is used to settle
routing and service costs.

## 9. Failure handling and recovery

- **Route expiry**: routes can expire and are re-discovered as needed.
- **Offline counterparties**: the payee retains the highest valid promise.
- **Disputes**: proof data can be submitted to the chain to commit or burn.
- **Chain reorgs**: SPV monitoring detects changes and updates wallet state.

## 10. Integration patterns

- **Web2 integration**: use UTOWallet SDK and HTTP API while IPv7 carries
  traffic in the background.
- **Service nodes**: deploy IPv7 relays or servers to provide bandwidth and
  routing services.
- **Merchant flows**: integrate UTOWallet for invoices, promises, and settlement
  without running a full chain node.

## 11. References

- UTOWallet consensus and API model:
  - https://github.com/utoid/utowallet/blob/main/CONSENSUS.md
- UTOWallet CLI and SDK usage:
  - https://github.com/utoid/utowallet/blob/main/USAGE.md
- IPv7 overview:
  - https://github.com/utoid/ipv7/blob/main/docs/OVERVIEW.md
