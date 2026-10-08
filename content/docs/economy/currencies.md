+++
title = "Game Currencies"
short = "Currencies"
weight = 1
date = "2026-10-08"
tags = ["credit", "ion", "shard", "economy"]
ShowToc = false
+++

Three currencies are available in Cyberbrawl:

**CREDIT** is the core currency: exclusively earned through playing the game such as completing daily quests, winning battles, tournaments, reward tracks, freely tradable on the blockchain.

**ION** is the crafting currency: made in [the Forge](/docs/economy/forge), at a price driven by smart contract from the CREDIT pool and the supply, and the only currency accepted for crafting and Hero Cores (summons).

**SHARD** is the premium currency: cosmetics, no ads, premium content that does not touch gameplay.

If you know Hearthstone, think Gold, Arcane Dust and Runestones, with two differences: Cyberbrawl currencies are freely tradable on the blockchain, and crafting is a live market controlled by smart contracts, not a fixed price list.

## Supply

The supply is 299,792,458 CREDIT. Each ranked season releases `5,000,000 × 0.98^season`; the schedule lands on the supply at season 122. Of each season's reward:

| Share | Goes to |
|---|---|
| 70% | The daily pool: 95% by quest weights, 5% to the Daily Top |
| 15% | The hourly spins |
| 15% | The season prizes: tournaments and boards |

Quests earn weights, the pool divides by those weights at the end of the day, a Boost multiplies your weights.

The Forge base is derived from the pool: CREDIT one claimant took per day over the last 14 days. Live at [`/forge/price`](/docs/data/api/#forge-price).

Live supply and earnings: [`/server/stats`](/docs/data/api/#server-stats).
