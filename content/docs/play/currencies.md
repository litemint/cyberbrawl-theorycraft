+++
title = "Game Currencies"
short = "Currencies"
weight = 3
date = "2026-10-08"
tags = ["credit", "ion", "shard", "economy"]
ShowToc = false
+++

Three currencies are available in Cyberbrawl:

**CREDIT** is the game's currency: earned only by playing, through daily quests, battles, tournaments and reward tracks.

**ION** is the crafting currency: the only currency used in crafting and Hero Cores (summons). It is exclusively made in [the Forge](/docs/play/forge).

**SHARD** is the premium currency: cosmetics, no ads, premium content that does not touch gameplay.

If you know Hearthstone, think Gold, Arcane Dust and Runestones, with crafting being a live market controlled by smart contracts, not a fixed price list.

## Supply

The supply of CREDIT is 299,792,458. Each ranked season releases `5,000,000 × 0.98^season`; the schedule lands on the supply at season 122. Of each season's reward:

| Share | Goes to |
|---|---|
| 70% | The daily bounty: 95% by quest weights, 5% to the Daily Top |
| 15% | The hourly spins |
| 15% | The season prizes: tournaments and boards |

Quests earn weights, the bounty divides by those weights at the end of the day, a Boost multiplies your weights.

The Forge base is derived from the bounty: CREDIT one claimant took per day over the last 14 days. Live at [`/forge/price`](/docs/data/api/#forge-price).

Live supply and earnings: [`/server/stats`](/docs/data/api/#server-stats).
