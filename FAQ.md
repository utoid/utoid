# UTOID FAQ

## General

### 1) What is UTOID?
UTOID is an identity-first system that combines an anonymous transport network
(IPv7), a settlement chain (utocoin), and a wallet layer (UTOWallet). It enables
private routing, low-latency off-chain payments, and on-chain finality when
needed.

### 2) What is the difference between UTOID and A7?
UTOID is the canonical identifier format across the system. A7 is the same
format used specifically as the IPv7 network address.

### 3) Is UTOID a blockchain or a network?
It is both. utocoin is the settlement chain, while IPv7 is the transport layer
that routes traffic and supports anonymous connectivity.

### 4) What is the current network status?
UTOID currently operates as a testnet. The focus is on protocol validation,
reliability, and developer integration.

## Wallet and payments

### 5) What is UTOWallet?
UTOWallet is the wallet daemon, CLI, and SDK that manage identity, stake,
cheques, promises, and synchronization. It connects to the chain via SPV.

### 6) Do I need to run a full node?
No. UTOWallet uses SPV connectivity, allowing users and applications to verify
critical chain data without operating a full node.

### 7) What are stake, cheque, and promise?
- **Stake**: on-chain collateral locked for a defined period.
- **Cheque**: on-chain UTXO used as a spendable payment unit.
- **Promise**: a signed off-chain commitment that references stake and cheque
  proofs.

### 8) How do off-chain payments remain safe?
Promises are signed and backed by on-chain stake. If a counterparty cheats, the
payee can submit an on-chain transaction to settle or burn stake under the
protocol rules.

### 9) Are off-chain payments instant?
Off-chain updates are designed to be low latency. Finality remains available on
chain when settlement is required.

### 10) What happens if a counterparty goes offline?
The payee retains the highest valid promise. If a settlement is required, the
payee can submit the appropriate on-chain transaction using the stored proofs.

## IPv7 network

### 11) How does IPv7 provide anonymity?
IPv7 uses neighbor-limited visibility and multi-hop routing. Each hop only sees
adjacent peers, and payloads are encrypted end to end.

### 12) How are routing fees handled?
Relays can quote prices per hop. UTOWallet accounts for routing costs and
settles with utocoin when payments are enabled.

### 13) Can IPv7 be used without payments?
Yes. IPv7 can be used purely as a transport layer. The payment layer is
optional depending on the application.

### 14) What are the IPv7 roles?
- **Peer**: participates in routing and forwarding.
- **Relay**: provides paid forwarding capacity.
- **Server**: hosts application endpoints on the network.

## Mining and economics

### 15) What proof-of-work algorithm is used?
utocoin uses scrypt proof-of-work.

### 16) What is the block time?
The target block time is 1 minute.

### 17) How does the halving schedule work?
The initial block reward is 50 coin. The reward halves every 2,100,000 blocks
(approximately 4 years) for three halvings. After the third halving, block
rewards remain constant.

### 18) What is the genesis allocation?
The total pre-allocation is 26,820,000 coin. 25% is reserved for the
foundation (locked for 2 years) and 75% for the genesis team (locked for 1
year).

## Governance and roadmap

### 19) Is UTOID fully decentralized?
UTOID is designed for open participation and community-driven evolution while
allowing pragmatic coordination where needed for performance and safety.

### 20) Will protocols evolve over time?
Yes. Protocol changes are expected to follow transparent review and versioned
releases. Details are documented alongside the corresponding implementations.

## Developer integration

### 21) Where should I start if I want to integrate?
Start with the UTOWallet documentation and the IPv7 overview, then review the
system architecture in this repository.

### 22) What APIs are available?
UTOWallet exposes authenticated HTTP and IPv7 APIs for payments, cheques,
stakes, sync, and status. The wallet SDK provides typed clients for common
workflows.

### 23) Does UTOID support Web2 integration?
Yes. The wallet API and SDK are designed to let traditional services adopt
UTOID features incrementally without rewriting their entire stack.

## Documentation

### 24) Where can I find the main docs?
- How UTOID works: https://github.com/utoid/utoid/blob/main/HOW_IT_WORKS.md
- White paper: https://github.com/utoid/utoid/blob/main/WHITE_PAPER.md
- UTOWallet docs: https://github.com/utoid/utowallet
- IPv7 overview: https://github.com/utoid/ipv7/blob/main/docs/OVERVIEW.md

### 25) How can I contribute?
See CONTRIBUTING.md in this repository for the process and expectations.
