+++
title = "Asset Ownership"
short = "Ownership"
weight = 3
date = "2026-10-10"
tags = ["stellar", "sui", "ownership", "cards", "vault", "credit", "ion"]
ShowToc = false
+++

Every card and the rank, quest or event that unlocks it: [see all cards and unlock ranks](https://cards.cyberbrawl.io).

Cards and in-game currencies can be moved freely between your game account and your onchain wallet.

Keep your assets in your in-game collection or hold them onchain, the choice is yours. Both options work seamlessly, giving you full custody and control over your assets.

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
