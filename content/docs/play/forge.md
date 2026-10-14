+++
title = "Crafting: The Forge"
short = "Crafting"
weight = 4
date = "2026-10-08"
tags = ["forge", "ion", "credit", "stellar"]
ShowToc = false
+++

## Rationale

Our goal was to create a crafting system that behaves like a living economy, honest by construction, with some play in it

In most card games, crafting is a price list: the studio decides what a card costs in dust and changes it when it likes. In Cyberbrawl, crafting is a live market driven by a smart contract.

The price of ION is not set by us. A smart contract on Stellar computes it from what players actually earned, the daily CREDIT bounty, and from how much ION exists, and it moves with the game, every day.

The contract is public, so anyone can verify an order: what you paid, how long it takes, what you get. Interaction is seamless for players, since the game handles contract calls and network fee.

## Lore

In the Cyberbrawl arena, everything is etched into silicon by ION plasma, from Hero Cores to card circuits.

Ionization takes time and energy. To prime the reaction chambers to `ignite`, you must prepay the Xenon fuel reserves and system's power grid with CREDIT. You can then `collect` the ION matrix once stabilized, or `extract` it early for a price.

The Forge is open to Forgemasters: reach Warlord in any season to earn the badge.

## Cost and time

An order of `amount` ION at `power` (1 to 24) costs and takes:

```
cost = amount × base × premium(power)
time = 172,800 s / power
premium(P) = P^(ln 3 / ln 24)
```

`base` is the price of one ION in CREDIT, published once a day from the daily bounty and its claimants, and moving at most 10% a day. The live value is [`/forge/price`](/docs/data/api/#forge-price).

A forge takes two days whatever the amount; only the power shortens it.

| Power | Time | Premium | Power | Time | Premium |
|---|---|---|---|---|---|
| 1 | 48 h | 1.000× | 8 | 6 h | 2.052× |
| 2 | 24 h | 1.271× | 12 | 4 h | 2.361× |
| 3 | 16 h | 1.462× | 16 | 3 h | 2.608× |
| 4 | 12 h | 1.615× | 20 | 2 h 24 | 2.817× |
| 6 | 8 h | 1.858× | 24 | 2 h | 3.000× |

All 24 steps: [contract README](https://github.com/litemint/cyberbrawl-contracts#cost-and-time-design). In the game, a service fee is added on top.

## Extract

A running forge can be pulled out before its time. The price is the difference between the power you paid and the power that would have finished right now, rounded up to the next step (nothing beats power 24):

```
now_power = ceil(172,800 s / elapsed)
cost = amount × base × (premium(now_power) − premium(power))
```

Example: 300 ION at power 1, base 24.24 CREDIT per ION. Ignite costs 7,272 CREDIT, ready in 48 hours. Extracting after 24 hours prices the forge as power 2: the step from 1.000× to 1.271× is 1,970 CREDIT. Total 9,242 CREDIT, what power 2 would have cost upfront.

## Links

- Contract: [`CDJZCLXBQ6QRRQIPOV73HXOL5HWZBDUWHRESMD23PORSFAGZD3ELZQMH`](https://stellar.expert/explorer/public/contract/CDJZCLXBQ6QRRQIPOV73HXOL5HWZBDUWHRESMD23PORSFAGZD3ELZQMH)
- Source and releases: [litemint/cyberbrawl-contracts](https://github.com/litemint/cyberbrawl-contracts)
