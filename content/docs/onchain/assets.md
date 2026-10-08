+++
title = "Assets on Stellar"
short = "Assets"
weight = 1
date = "2026-10-08"
tags = ["stellar", "assets", "cards"]
+++

Cyberbrawl assets issuance follows SEP-1 and [SEP-39](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0039.md), the interoperability guideline for NFTs on Stellar.

The Stellar TOML is available here: [`cyberbrawl.io/.well-known/stellar.toml`](https://cyberbrawl.io/.well-known/stellar.toml).

## Cards

A card is a classic Stellar asset that can be held in any Stellar wallet. One card is one stroop, the smallest unit of the asset.

Cards owned onchain are never custodied by the game. The playable set of an account is its unlocked cards plus whatever card assets its linked wallet holds, read directly from the chain. Buy a card on the DEX and it is in your deck at the next refresh; sell it and it leaves.

## Where they trade

- [The Undercity](https://undercity.cyberbrawl.io): the game's dedicated market, every card in USDC, XLM or CREDIT.
- [market.litemint.com](https://market.litemint.com): the Litemint marketplace.
- Any Stellar DEX or wallet, since they are regular Stellar assets.

The quotes, found on the DEX by `path`, are public: [`/listings/prices`](/docs/data/api/#market-prices).

