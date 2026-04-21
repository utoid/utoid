# Glossary

- **UTOID**: The canonical identifier format used across the system for
  identity, authorization, and routing.
- **A7**: The same identifier format used specifically as the IPv7 network
  address.
- **utocoin**: The settlement chain and native asset used for routing and
  payments.
- **IPv7**: Anonymous, multi-hop transport network addressed by A7.
- **UTOWallet**: Wallet daemon, CLI, and SDK that manage identity, payments,
  and SPV connectivity.
- **walletd**: The long-lived wallet service that exposes APIs and manages
  local state.
- **SPV**: Simplified Payment Verification, used by wallets to verify chain
  data without running a full node.
- **Stake**: On-chain collateral locked for a defined period. Used to secure
  off-chain promises.
- **Cheque**: On-chain UTXO used as a spendable payment unit in promises.
- **Promise**: Signed off-chain commitment referencing stake and cheque proofs.
- **Relay**: An IPv7 node that forwards traffic for other peers and may charge
  for bandwidth.
- **Peer**: A node participating in IPv7 routing and discovery.
- **Server**: An IPv7 node that hosts application endpoints.
- **Commit**: The on-chain action that finalizes a cheque-based payment.
- **Burn**: The on-chain action that penalizes misbehavior by consuming stake
  under the promise rules.
