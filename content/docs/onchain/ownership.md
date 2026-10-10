+++
title = "Asset Ownership"
short = "Ownership"
weight = 3
date = "2026-10-10"
tags = ["stellar", "ownership", "cards", "vault", "credit", "ion"]
ShowToc = false
+++

Every card and the rank, quest or event that unlocks it: [see all cards and unlock ranks](https://cards.cyberbrawl.io).

Cards and in-game currencies can be moved freely between your game account and your onchain wallet.

Keep your assets in your in-game collection or hold them onchain, the choice is yours. Both options work seamlessly, giving you full custody and control over your assets.

## Cards

**Withdraw to Stellar**

To withdraw a card to your Stellar wallet:

- Link your wallet in the Cyber Vault.
- Add a trustline for the card's asset.
- The game will automatically send the card to your wallet.
  
Once withdrawn, the card is removed from your in-game collection and can be played directly from your wallet.

In-game currencies can also be withdrawn through the Cyber Vault.

**Deposit from Stellar**

To deposit a card into your game account, send it to the issuer account below, using your `Battle ID` as the transaction memo.

Issuer account: `GBAKUWF2HTJ325PH6VATZQ3UNTK2AGTATR43U52WQCYJ25JNSCF5OFUN`

The payment operation burns the onchain asset, and the game issues it to your game account. The card becomes available to play after the next refresh.

You can also deposit any amount of CREDIT, ION, or SHARD using the same process.

## Rules worth knowing

- The memo is mandatory and must be your Battle ID. A payment without it cannot be credited.
- A payment to the issuer burns the asset. There is no automatic refund: if something went wrong, contact support with the transaction hash.
- One card is one stroop (`0.0000001`).
