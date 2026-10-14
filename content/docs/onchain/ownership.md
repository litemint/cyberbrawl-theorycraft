+++
title = "Asset Ownership"
short = "Ownership"
weight = 1
date = "2026-10-10"
tags = ["stellar", "sui", "ownership", "cards", "vault", "credit", "ion"]
ShowToc = false
+++

Your cards and your currencies are yours. In the game they live on your account, like in any game you know. When you want more than that, you can take them onchain: keep them in a wallet only you control, trade them for USDC and other currencies, sell them on any marketplace, give them to a friend, or bring them back to the game.

That is what the blockchain adds to Cyberbrawl: full ownership, opt in, never required. The game plays the same either way.

What ownership gives you:

- Nothing depends on us. A card you hold onchain stays yours whatever happens to Cyberbrawl.
- A market with real prices, open to anyone, instead of a studio's price list.
- A collection that goes where you go: any wallet, any marketplace that reads the chain.

Cyberbrawl supports two networks, [Stellar](https://stellar.org/) and [Sui](https://www.sui.io/). Every card and the rank, quest or event that unlocks it: [see all cards and unlock ranks](https://cards.cyberbrawl.io).

## How to transfer cards

### The simplest way

- Open [the Undercity](https://undercity.cyberbrawl.io) from the game link, you are logged in.
- Go to **My Cards** and connect any Stellar or Sui wallet.
- Drag a card between the game and the wallet, in either direction.

### Advanced users

Advanced users can do the same with any blockchain tool of their choice, a wallet, a DEX or a script. A few rules to know:

- On Stellar the memo is mandatory and must be your Battle ID. A payment without it cannot be credited.
- A payment to the issuer burns the asset and credits your in-game account. There is no automatic refund: if something went wrong, contact support with the transaction hash.
- On Stellar one card is one stroop (`0.0000001`). On Sui one card is one object.
- On Sui the deposit is a transaction your wallet signs, so it carries your Battle ID itself and needs no memo.

## Under the hood

### On Stellar

A card is a classic Stellar asset that can be held in any Stellar wallet; one card is one stroop, the smallest unit of the asset. Issuance follows SEP-1 and [SEP-39](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0039.md), the interoperability guideline for collectibles on Stellar. The Stellar TOML: [`cyberbrawl.io/.well-known/stellar.toml`](https://cyberbrawl.io/.well-known/stellar.toml).

Cards held onchain are never custodied by the game. The playable set of an account is its unlocked cards plus whatever card assets its linked wallet holds, read directly from the chain. Buy a card on the DEX and it is in your deck at the next refresh; sell it and it leaves.

Where they trade:

- [The Undercity](https://undercity.cyberbrawl.io): the game's dedicated market, every card in USDC, XLM or CREDIT.
- [market.litemint.com](https://market.litemint.com): the Litemint marketplace.
- Any Stellar DEX or wallet, since they are regular Stellar assets.

The quotes, found on the DEX by `path`, are public: [`/listings/prices`](/docs/data/api/#market-prices).

### On Sui

The Move package: [github.com/litemint/cyberbrawl-contracts](https://github.com/litemint/cyberbrawl-contracts), `0xc0ecc184efcc2605e55b24afe103dc9d88c7e4cdc918061fcbe42d4f81fe32c3` on mainnet. Cards are objects of type `…::card::Card`. Every card sits in a Kiosk under a transfer policy with a lock rule, and a royalty rule applied to every sale.

Where they trade:

- [The Undercity](https://undercity.cyberbrawl.io): the game's dedicated market, listings priced in SUI.
- Any Sui marketplace or wallet that reads Kiosk listings.

The listings are public: [`/sui/market`](/docs/data/api/#sui-market).
