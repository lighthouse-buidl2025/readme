# PersonaChain AI

## Project Overview

PersonaChain AI is a Web3 data infrastructure project that analyzes on-chain data to define behavioral profiles ("personas") for each wallet and uses AI agents to automatically recommend monetization strategies based on these personas.

We extract user behavioral characteristics from massive on-chain logs in Web3. By analyzing transaction patterns, asset distribution, and interaction frequency, we categorize wallets into personas such as Explorer, Diamond Hands, Whale, and Degen. Each persona receives tailored strategy recommendations.

---

## Architecture Overview

PersonaChain is designed as a modular AI-driven system connected through a unified Gateway API. It integrates distinct services under the following structure:

### 1. Modules

- **Persona Engine**: Performs wallet analysis and persona classification.
- **User Module**: Handles user profile, email, and telegram linkage.
- **Tx Agent**: Creates and executes transactions and defines automated execution rules.
- **Eliza Agent**: Interfaces with AI chat agents for user queries.

### 2. Gateway API

Acts as a centralized access point across modules. All requests are routed through `http://localhost:8000/api`.

---

## Core Features

### Wallet Persona Classification

- Analyze wallet activity based on on-chain transactions, token holdings, NFTs, and DeFi interactions.

### AI-Based Strategy Recommendation

- Automatically suggest optimal strategies such as airdrop hunting, yield farming, or high-volume trades.

### Real-Time Wallet Analysis API

- REST API provides real-time or cached wallet insights, including percentile scoring and persona type.

### Scoring and Clustering

- Cluster wallets by behavior similarity and normalize incoming data against a dataset of 1000+ wallets.

---

## Wallet Analysis Data Schema

### Basic Information

| Field | Type | Description |
| --- | --- | --- |
| wallet | String | Wallet address |
| balance | Number | ETH balance (Wei) |
| use_stable | Boolean | Uses stablecoins |
| tokens_count | Integer | Number of tokens interacted with |
| recent_transactions_count | Integer | Recent 6-month transaction count |

### Transaction Information

| Field | Type | Description |
| --- | --- | --- |
| transactions | Array | Recent transaction list (deduplicated) |
| transactions[].method | String | Function signature |
| transactions[].contract_address | String | Contract address |
| total_transactions | Integer | Total transactions |
| average_gas_fee_eth | Float | Avg. gas fee in ETH |
| total_gas_fee_eth | Float | Total ETH spent on gas |
| max_gas_fee_eth | Float | Max gas for a single transaction |
| most_active_hour | Integer | Most active hour (0–23) |
| average_transaction_interval_days | Float | Avg. transaction interval in days |

### NFT Information

| Field | Type | Description |
| --- | --- | --- |
| owned_nfts_count | Integer | Total NFTs held |
| owned_nft_collections_count | Integer | NFT collection count |
| owned_nft_collections | Array[String] | NFT collection symbols |

### FT (Token) Information

| Field | Type | Description |
| --- | --- | --- |
| token_count | Integer | Number of ERC20 tokens |
| token_details | Array | Token details per asset |
| token_details[].token | String | Token symbol |
| token_details[].balance | Float | Token balance |
| token_details[].holding_period_days | Float | Holding period in days |
| token_details[].net_flow | Float | Net inflow (received - sent) |

### DEX Activity

| Field | Type | Description |
| --- | --- | --- |
| dex_volume_usd | Float | Total DEX volume (USD) |
| dex_count | Integer | Number of DEX platforms used |
| dex_list | Array[String] | DEX platform names |

---

## Persona Scoring Table

| Parameter | Explorer | Diamond | Whale | Degen | Description |
| --- | --- | --- | --- | --- | --- |
| distinct_contract_count | 4 | 1 | 0 | 1 | Explorer prefers diversity |
| dex_platform_diversity | 2 | 1 | 0 | 4 | Degen prefers variety |
| avg_token_holding_period | 0 | 5 | 2 | 0 | Diamond holds longer |
| transaction_frequency | 1 | 0 | 1 | 3 | Degen trades more |
| dex_volume_usd | 0 | 1 | 5 | 2 | Whale trades high volume |
| nft_collections_diversity | 3 | 2 | 2 | 1 | Explorer values diversity |

### Persona Summary

- **Explorer**: High contract and NFT diversity
- **Diamond**: Long-term holders
- **Whale**: High transaction volume
- **Degen**: High frequency and DEX diversity

---

## Tech Stack

- **Frontend**: Next.js
- **Backend**: Go, TypeScript, Express.js, MongoDB, SQLite (selectively used based on context)
- **AI Engine**: Eliza OS Agents, GPT-4o
- **On-chain Sources**: Alchemy, Bitquery, Etherscan APIs

---

## Setup

```
pnpm install
pnpm run start
```

### .env Configuration

```
ETHERSCAN_API_KEY=xxxx
ALCHEMY_API_KEY=xxxx
BITQUERY_API_KEYS=aaa,bbb
PORT=8021
```

---

## Roadmap

### 1. User Onboarding & Initial Data Collection

- Wallet connection and automated on-chain data collection
- Multi-chain support (Ethereum, NEAR, Story, etc.)
- Consent flow for data collection and privacy protection

### 2. Data Sufficiency Validation

- Automatic logic to determine if sufficient data is available
- Provide customized feedback and request more input if necessary

### 3. Advanced Persona Analysis Engine

- Develop a persona framework based on 4 core indicators:
    - Explorer
    - Diamond hands
    - Whale
    - Degen
- Scoring interface with detailed explanation for each indicator

### 4. Insight & Service Recommendation System

- Visualize cluster analysis with similar wallet users
- Persona-based protocol and service matching engine
- Automated suggestions for improving Web3 activity

### 5. AI Agent Automation & Execution Framework

- Leverage Eliza OS Agents to turn persona insights into automated Web3 actions
- Enable intelligent task automation such as optimal trade timing, gas fee optimization, and rebalancing based on user profiles
- Each agent is deployed modularly on SAGA to execute wallet-specific strategies
- Eliza agents continuously learn from on-chain behavior to refine and personalize the automation loop

### 6. Expansion & Commercialization

- NFT issuance for persona certification and community use
- B2B API commercialization for enterprises
- Full-stack SaaS integration for persona analysis, insights, and automation


### Deployed @ SEPOLIA
Deployer: 0xAF7fBBFE990427B0eC8Cc477f9466Aedfc3d2717
AccountImpl: 0x4402d073ea722AB69879Be1fC1F1C22CBc96C261
Core: 0xbcCC18aa7227723Accd4A95c290605cEE4cb946A

tx links : https://sepolia.etherscan.io/address/0xbcCC18aa7227723Accd4A95c290605cEE4cb946A

### Deployed @ SAGATESTNET
Deployer: 0x77777777C54FD7A001F50fa752e524ec9B08A487
AccountImpl: 0x7a0b710ed5D0D2F708Af491F6D3dcff5D872EDef
Core: 0xdd5F1B42A9caa4883d685bD218CF3a9C08622FEb

tx links : 
✅  [Success] Hash: 0x254f884a4ecf6a33c0407dd76f4cfe1ab2e55bdf9fc8af9f757261c30bdd2113
Contract Address: 0x7a0b710ed5D0D2F708Af491F6D3dcff5D872EDef
Block: 77
Paid: 0.000000073444057944 ETH (1048422 gas * 0.000070052 gwei)

✅  [Success] Hash: 0x2b8652125a6780f967264edb0e0c84f56a2bc807e74d303da28f7a2a3ad9fc73
Contract Address: 0xdd5F1B42A9caa4883d685bD218CF3a9C08622FEb
Block: 77
Paid: 0.000000061387198068 ETH (876309 gas * 0.000070052 gwei)

### Deployed @ ROOTSTOCKTESTNET
Deployer: 0x77777777C54FD7A001F50fa752e524ec9B08A487
AccountImpl: 0x046A8BB2C22Be6c749EeA89dd38da33565f3Aea4
Core: 0x994c9936a10f2DD4bb8569a4D6C2D06F3D3F749d

tx links : 
✅  [Success] Hash: 0x466dad4549d2d58e629fa67701669215e1dbf601adfcdd67867b9df5c2f1ef79
Contract Address: 0x994c9936a10f2DD4bb8569a4D6C2D06F3D3F749d
Block: 6271711
Paid: 0.000005331907158705 ETH (872889 gas * 0.006108345 gwei)

✅  [Success] Hash: 0xa3440d6504330235c81fad5572d05c2967c652ae9b1b53d9710238fad88bc132
Contract Address: 0x046A8BB2C22Be6c749EeA89dd38da33565f3Aea4
Block: 6271711
Paid: 0.00000640590691833 ETH (1048714 gas * 0.006108345 gwei)
