# Dragon Staking Program

A Solana NFT staking smart contract built using the Anchor framework.  
The program allows users to stake Dragon NFTs and earn SPL token rewards based on NFT rarity, staking duration, and bonus point systems.

---

# Overview

Dragon Staking is a GameFi-style staking protocol designed for NFT collections on Solana.  
Users can lock NFTs into the staking vault and receive rewards over time depending on several scoring mechanisms.

The project includes:

- NFT staking and unstaking
- SPL token reward distribution
- Rarity-based reward multipliers
- Long-term staking bonuses
- Gang creation bonus system
- User staking pools
- Global reward vault management

---

# Features

## NFT Staking

Users can:

- Stake Dragon NFTs
- Unstake NFTs anytime
- Track staking data per NFT
- Participate in long-term reward systems

---

## Reward System

Rewards are distributed using:

- NFT rarity points
- Duration bonus points
- Account verification bonus
- Global staking pool statistics

Rewards are claimable in SPL tokens.

---

## Gang Bonus System

When a user stakes at least 3 NFTs:

- The account becomes eligible for duration bonuses
- Staking duration starts tracking automatically
- Long-term holders receive higher multipliers

---

# Program Architecture

## GlobalPool

Stores global staking statistics.

### Data

- Total staked NFTs
- Total rarity points
- Duration bonus points
- Reward token balances
- Allocated rewards

---

## UserPool

Stores staking information for each user.

### Data

- Wallet owner
- Staked NFT count
- Claimable rewards
- Earned rewards
- Daily rewards
- Bonus points
- Gang creation timestamp

---

## UserPoolData

Stores per-NFT staking records.

### Data

- NFT mint address
- NFT owner

---

# Instructions

## Initialize Global Pool

Initializes the global staking vault and statistics account.

```rust
initialize()
```

---

## Initialize User Pool

Creates a staking pool for a user.

```rust
init_user_pool()
```

---

## Stake NFT

Transfers NFT from user wallet into the staking vault.

```rust
stake_nft(rarity)
```

### Effects

- Increases staking counters
- Adds rarity points
- Starts gang timer if user owns 3+ NFTs

---

## Unstake NFT

Returns NFT back to the user.

```rust
unstake_nft(global_bump, rarity)
```

### Effects

- Removes rarity points
- Updates staking totals
- Removes duration bonuses if staking count drops below 3

---

## Claim Rewards

Transfers claimable SPL rewards to the user.

```rust
claim_reward()
```

---

## Deposit Reward Tokens

Deposits SPL tokens into the reward vault.

```rust
deposit_token(amount)
```

---

## Withdraw Reward Tokens

Withdraws tokens from the reward vault.

```rust
withdraw_token(amount)
```

---

## Calculate Daily Rewards

Calculates rewards based on total staking points.

```rust
calc_daily_reward()
```

---

## Calculate Duration Bonus

Applies bonus points based on staking duration.

```rust
calc_duration_bonus()
```

---

# Reward Logic

The reward system distributes rewards proportionally.

## Formula

```text
daily_reward =
available_token_amount
/ 12
/ 30
/ total_points
* user_points
```

---

# Duration Bonus Table

| Staking Duration | Bonus |
|------------------|--------|
| 0 - 30 days      | -5     |
| 30 - 60 days     | +5     |
| 60 - 90 days     | +15    |
| 90 - 180 days    | +30    |
| 180+ days        | +50    |

---

# Tech Stack

- Solana
- Rust
- Anchor Framework
- SPL Token Program

---

# PDA Accounts

## Global Authority

```rust
GLOBAL_AUTHORITY_SEED
```

Used for:

- Reward vault authority
- NFT vault authority
- Program signing

---

# Security Notes

This project is currently a prototype implementation and should be audited before production deployment.

## Known Concerns

- NFT metadata verification is missing
- Rarity values are user-provided
- Some arithmetic operations are unchecked
- Token account validations are limited
- Administrative permissions are not fully restricted

---

# Future Improvements

- Metaplex metadata verification
- Collection validation
- On-chain rarity system
- Admin role management
- Reward emission scheduler
- APR/APY calculations
- Frontend dashboard
- Automated reward distribution

---

# Example Workflow

## User Flow

1. Initialize user pool
2. Stake NFTs
3. Earn rewards over time
4. Claim SPL rewards
5. Unstake NFTs anytime

---

# Build & Deploy

## Install Dependencies

```bash
cargo build
anchor build
```

---

## Deploy

```bash
anchor deploy
```

---

## Run Tests

```bash
anchor test
```

---

# Program ID

```text
Bnmuo5aGbvhwUGYkkZydyxgsyPNuXNL9GhkVH6XpKnu1
```

---

# License

MIT License

---

# Disclaimer

This software is provided as-is without warranties.  
Use at your own risk.
