# Liquidity Layers

Lex operates on a prioritized multi-layered liquidity framework to maximize efficiency and scalability.

### Layer 1: Coincidence of Wants (USP)

Coincidence of wants leverages natural liquidity movements between chains.

**Example:**

* **Scenario:** A solver operating on Polygon and Solana has $170,000 on Solana and $30,000 on Polygon. A market maker has excess liquidity on Polygon and needs liquidity on Solana.
* **Solution:** Lex matches these liquidity needs, enabling direct on-chain transfers without bridging, utilizing Solana’s SVM for low-latency execution.

This layer handles simple and complex matching scenarios, including multi-asset swaps and multi-party transactions.

### Layer 2: Micro Liquidity Pools (USP)

Micro liquidity pools provide dynamically rebalanced liquidity across chains.

* **Capital Efficiency:** Pools are highly optimized, focusing on stablecoins and native chain assets (e.g., SOL, ETH, MATIC).
* **Automated Rebalancing:** Lex manages pool rebalancing periodically, ensuring high liquidity utilization and minimal latency.
* **Use Case:** A solver supplies liquidity on one chain and accesses the same amount on another chain in seconds to fulfil an intent.

### Layer 3: External Solvers (Open Market)

Lex integrates with existing solver networks and protocols to provide additional liquidity options.

* **Auction Mechanism:** Intent auctions allow external solvers to bid, ensuring optimal liquidity and output.
* **Collaboration:** Enables external solvers, bridges, and intent protocols to participate without relying on Lex’s native pools.

### Layer 4: Compass Integration (Backup)

Compass, the flagship product of Blockend, acts as a liquidity aggregator.

* **Aggregated Liquidity:** Sources liquidity from DEXs, bridges, RFQ providers, and intent protocols.
* **Fallback Mechanism:** If internal layers cannot fulfill an intent, Compass ensures execution through its broad liquidity network.

***

### Workflow

1. **Intent Submission:** A user or protocol submits a cross-chain liquidity intent.
2. **Auction Process:** Lex’s SVM layer initiates an auction across its four liquidity layers.
3. **Execution:** The most efficient liquidity source is selected, ensuring optimal output and speed.
4. **Rebalancing:** Post-transaction, Lex rebalances liquidity across chains to maintain efficiency.
5. **Settlement:**  Settlement data from multiple transactions is efficiently compressed and securely posted to the Solana Mainnet, ensuring transparency and composability.

