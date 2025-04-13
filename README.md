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

## Team

- Yeonha Park — Blockchain Developer & AI Pipeline Lead
- Yeonha Park — Blockchain Developer & AI Pipeline Lead
- Yeonha Park — Blockchain Developer & AI Pipeline Lead
- Yeonha Park — Blockchain Developer & AI Pipeline Lead
- [Additional team members to be added]

---

## Tech Stack

- **Backend**: Python (FastAPI), PostgreSQL, Supabase
- **AI Engine**: GPT-4o, persona-based scoring, clustering
- **On-chain Sources**: Alchemy, Bitquery, Etherscan APIs
- **Infrastructure**: Vercel, Docker, Ubuntu

---

## Setup

```
npm install
npm run dev
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

- Launch AI transaction agents on SAGA
- NFT issuance of wallet personas for gamification
- Advanced behavior prediction models
- API commercialization for B2B wallet platforms
