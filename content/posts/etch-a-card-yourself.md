+++
title = "Etch a Cyberbrawl Card with Zero-Knowledge on Stellar"
date = "2026-10-28T09:00:00+09:00"
slug = "etch-a-cyberbrawl-card-with-zero-knowledge-on-stellar"
draft = false
description = ""
summary = "In the game, etching a card takes one tap: no wallet, no fee to sign, no proof to build. The game calls a public smart contract on Stellar for you. Want to do it yourself? Here is how."
tags = ["cyberbrawl", "stellar", "soroban", "zero-knowledge", "crafting"]
categories = ["technology", "gaming"]
authors = ["kyungjin"]
authorDisplay = ["Fred Kyung-jin Rezeau"]
[cover]
image = "/img/banner.png"
alt = "etch-a-card-yourself"
relative = false
hidden = true
+++

In Cyberbrawl, forging ION and crafting cards is as simple as pressing a button in the Forge. No wallets, fees, or proofs to worry about. The game handles everything seamlessly, so every player can enjoy the experience without knowing anything about blockchain.

Behind the scenes, real transactions take place onchain. When a card is gated, the game generates a zero-knowledge proof and etches the card through the Beam, a public smart contract on Stellar. Every call is independently verifiable.

But you don't have to go through the game. You can interact with the Beam directly, using your own wallet. This article shows you how.

Alternatively, you can follow along with this video:

{{< youtube pLJbe--LH5s >}}

## What you need

- The [Stellar CLI](https://developers.stellar.org/docs/tools/cli) and an account with a key you can sign with, holding some XLM and the ION to spend (`ION`, issued by `GBAKUWF2HTJ325PH6VATZQ3UNTK2AGTATR43U52WQCYJ25JNSCF5OFUN`).
- For Epic and Legendary cards only: [Node.js](https://nodejs.org) 22.12 or newer, and your Engram (see step 4).

In the commands below, `GYOU…` is your account's address and `you` is the name of its key in the CLI.

## 1. Pick a card

Every card that can be etched, with its ION price:

```bash
curl https://connect.cyberbrawl.io/beam/cards
```

The example below etches Energy Wave, `card_02_00046`. The asset of a card is `CARD` plus the five digits of its id, here `CARD00046`.

## 2. Add the trustline

The card lands in your account as a regular Stellar asset, so the account needs a trustline to it first:

```bash
stellar tx new change-trust --network mainnet --source-account you \
  --line CARD00046:GBAKUWF2HTJ325PH6VATZQ3UNTK2AGTATR43U52WQCYJ25JNSCF5OFUN
```

## 3. Get a quote

The contract only etches at a price the game has signed. Ask for the quote of your card, for the address that receives it:

```bash
curl "https://connect.cyberbrawl.io/beam/quote?card=card_02_00046&receiver=GYOU…" > quote.json
```

```json
{
  "contract": "CDQNFEV6NNDEF2PEDI3MBBKZ4G6XBXNZTRB55KUZUDYLA42PI4ZK2XJS",
  "card": "card_02_00046",
  "receiver": "GYOU…",
  "price": 900,
  "tier": 1,
  "expires": 1793074144,
  "attestation": "434248595a43…"
}
```

`price` is the ION burned, `tier` is 0 for a Common card and 1 for Epic and Legendary, and the quote is good for 30 minutes (`expires` is a Unix time).

## 4. Prove it (Epic and Legendary only)

Epic and Legendary cards are etched only by players who defeated the Ironclad. The contract does not look at your game account: you show it a zero-knowledge proof made from your Engram. A Common card needs no proof, skip to step 5.

In the game, go to **Options > Advanced > Generate Your Digital Engram** and save the file as `engram.json`. The proof is made on your machine, your Engram never leaves it.

```bash
npm install snarkjs circomlibjs @stellar/stellar-sdk
curl -O https://raw.githubusercontent.com/litemint/cyberbrawl-contracts/main/circuits/circom/engram/prove.js
curl -O https://raw.githubusercontent.com/litemint/cyberbrawl-contracts/main/circuits/circom/engram/artifacts/engram.wasm
curl -O https://raw.githubusercontent.com/litemint/cyberbrawl-contracts/main/circuits/circom/engram/artifacts/engram.zkey
```

`engram.wasm` and `engram.zkey` are the compiled circuit and its proving key, the same ones the game uses.

```bash
node prove.js engram.json GYOU… engram.wasm engram.zkey > proof.hex
```

It takes a few seconds and prints 288 bytes as hex. The address must be the receiver you asked the quote for: the proof is bound to it.

## 5. Etch

A Common card has no gate, so the contract ignores the proof. The CLI still wants a value for it, so pass `00`:

```bash
stellar contract invoke --network mainnet --source-account you \
  --id CDQNFEV6NNDEF2PEDI3MBBKZ4G6XBXNZTRB55KUZUDYLA42PI4ZK2XJS -- etch \
  --payer GYOU… \
  --attestation "$(jq -r .attestation quote.json)" \
  --proof 00
```

For an Epic or Legendary card, pass the proof from step 4 instead: `--proof "$(cat proof.hex)"`.

The ION is burned from your account and the card lands on the receiver of the quote. If the card is out of stock the call fails and nothing is burned.

## In the game

If the receiver is the `G` address linked to your account, the card is playable right away. With any other address the card is yours all the same, and you can deposit it into the game yourself later.

The contract and the circuit are public: [cyberbrawl-contracts](https://github.com/litemint/cyberbrawl-contracts).
