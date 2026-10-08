+++
title = "Fun Does Not Need Finality: Blockchain Game Design with Cyberbrawl on Stellar"
date = "2025-11-23T00:09:35+09:00"
slug = "blockchain-game-design-cyberbrawl-stellar"
draft = false
description = ""
summary = "The heart of a game experience never lives on layer zero. In this article I reflect on how Cyberbrawl was built to preserve play with blockchain."
tags = ["game", "design", "blockchain", "cyberbrawl"]
categories = ["technology", "gaming"]
authors = ["kyungjin"]
authorDisplay = ["Fred Kyung-jin Rezeau"]
[cover]
image = "/img/banner.png"
alt = "blockchain-game-design-cyberbrawl-stellar"
relative = false
hidden = true
+++

Regardless of scale, shipping a game is always a challenge that requires a precise balance of art and engineering. Over time, I have come to think that game design is to software what storytelling is to language.

{{< extlink "https://cyberbrawl.io" "Cyberbrawl" >}}, my latest project, was no exception. It pushed me at *every turn*, even more so with the extra layer of building on {{< extlink "https://developers.stellar.org/" "Stellar" >}} where onchain experimentation rarely comes with a blueprint.

However, I strongly believe that while blockchain adds intriguing possibilities, it doesn't alter how a game's core is actually built.

{{< youtube 7uv2sxj_hqA >}}
*Cyberbrawl: Build Your Tournament Decks, Enroll & Compete!*

## Hype Is Not a Game Loop

I still see many blockchain games treating the chain itself as source of meaningful participation with teams obsessing over tokens, mint schedules and economies before they have anything playable. That mindset has produced a whole ecosystem of onchain (*sic, vanity*) metrics.

This approach may help create the initial burst of hype. But the truth is that working backward from hype into a coherent game is extremely hard. A few manage it (e.g., the {{< extlink "https://www.nomanssky.com/" "No Man's Sky" >}} turnaround miracle) but those are the exception.

Hype-first design is a huge bet; and I would rather know the game before going all in.

## The Core Loop Is Still the Only Layer That Matters

A game reveals its core early; that's why I always start with the simplest prototypes. They help in two important ways:
- The creative process constantly tempts you with illusions: another clever mechanic, another cool feature. Scoping discipline helps, but the real shortcut is trusting prototypes over ideas.
- Once you have a playable prototype, you begin to notice the things that matter like tension, resolution, depth. When the core loop works, every other layer (graphics, content, effects...) becomes leverage.

And this applies to any project size. In fact, the smaller the loop, the harder the craft because tension lives in thinner margins. Just a small gravity tweak in {{< extlink "https://flappybird.io/" "Flappy Bird" >}}, an increased spawn rate in a tower defense, can completely break the game.

My projects have always reminded me that the core loop is nonnegotiable.

Cyberbrawl also started with a simple prototype, no fancy graphics, no effects, no blockchain. If the core loop doesn't work, no amount of production or extra layers can fix it.

## Play Transcends Layer Zero

Play is not a universal language because it resonates differently based on the audience. That's why my first question is always: **who is this game for?** 

Most of my design choices for Cyberbrawl were shaped by the answer to this question. The game sits inside a TCG framework, a genre that typically appeals to midcore or hardcore players—but I wanted it closer to casual-midcore, a space that feels more web-native and less niche.

As a longtime {{< extlink "https://hearthstone.blizzard.com/" "Hearthstone" >}} fan, I am familiar with the genre rituals: long turns, meta knowledge, punishing Legend rank grinding. Those hardcore elements are engaging for most TCG players but none survive a casual audience. Knowing your players is not optional.

{{< youtube dEnO4dJTRag >}}
*Climb to Legend Rank – Hearthstone – full stream on {{< extlink "https://www.youtube.com/@kyungjin" "my channel" >}}*

I was in a meeting with a major Korean game publisher looking to move into blockchain, and they asked me which chain players prefer, or why I picked Stellar. The truth is, ETH vs Solana vs Immutable is merely noise. It does nothing to define your target audience because the heart of a game experience never lives on layer zero. And in fact, no amount of onchain polish can replace knowing what players come for.

I actually think major publishers are the best positioned to push this space forward precisely because they deal with real games, real players.

## Play Is Crafted, Not Minted

Cyberbrawl was forged from day one for that casual-midcore, web-native audience.

The first requirement was: no broken decks. I wanted players to be able to jump into a match without needing *meta* knowledge or spreadsheets, right after clicking the *Play* button. So, the {{< extlink "https://github.com/litemint/cyberbrawl-community-resources/blob/master/deck-shuffle.md" "shuffle algorithm" >}} was built to avoid clumping and enforce functional curves. 

The energy system came from the same mindset. In Cyberbrawl, energy creates a natural pressure curve instead of leaning on the usual mana tax. It is transient. You can drain it, coalesce it, redistribute it. That fluidity gives all cards built-in comboability (e.g., Barricade can convert Biohazard Damage into Armor) and turns the hand into an *energy surface*. Casual players can read this system very easily, while midcore players find plenty of tactical depth in the flows.

It is easy for blockchain games to lean too heavily on tokens and onchain mechanics, but that rarely aligns with what a real game audience wants. When engagement is built around tokens and transactions rather than a crafted play experience, the result speaks to crypto users rather than players.

## Do Not Gas Your Game Out

Flow is fragile. And blockchain adds a lot of friction via consensus delays, security requirements, *ad hoc* UX. Even 5 second finality on Stellar is too disruptive inside a core loop. That's why, when designing Cyberbrawl, I made sure the loop never needed blockchain.

And this extends beyond games. Take the hype around the {{< extlink "https://www.x402.org/" "x402 protocol" >}}, it's easy to imagine an army of x402-enabled AI agents stuck waiting on micropayment confirmations. That design (or lack of) also assumes that agents can't simply decouple payment from execution. Honestly, simple recurring subscriptions give you proper encapsulation: more flexible, more secure, more scalable, and with no latency.

In my experience, crossing layer boundaries without proper encapsulation tends to cause problems. Essentially, if you drag consensus into your game loop, the experience will suffocate.

Now I believe that when blockchain is kept at the right layer, properly encapsulated, it strengthens and enables use cases never possible before: ownership, permanence, identity, provability, payments.

And practically, platforms like {{< extlink "https://developers.stellar.org/" "Stellar" >}}, with their focus on cost-efficiency and speed, allow us to achieve this *quietly in the background*.

## Players Want Fun

As players, we remember fun. That's why the cycle of tension and resolution is so important in games.

In Cyberbrawl, the entire roster is shaped around it. Overload cards create explosive tempo spikes, Biohazard and Shockwave deliver the big-number bursts players love (or hate), drain cards punish greed, Overclock expands the *energy surface* for late-game swings. Every component is there to support the emotional peaks that make a match stay with us.

By contrast, I have seen plenty of blockchain reward models trying to atomize fun into micro-ticks. They confuse frequency with tension. What keeps me jumping back, seasons after seasons, into the PvP madness of rated Arena in World of Warcraft, is uncertainty, anticipation, the surge.
{{< youtube WmeHOTWgZjU >}}
*PvP Rated Arena, Season 3*

Fun doesn't require finality. Minting cards before the game is like printing Olympic medals before deciding the discipline and the rules.

## Blockchain Is the Continuity Layer

Now blockchain finality can preserve what fun produces, as long as it does not disrupt the loop that orchestrates fun in the first place.

I believe that blockchain shines when it quietly extends the player's experience beyond the game:
- letting achievements, progress, skill, and reputation cross over to new experiences.
- giving players decentralized ownership over the items they earn, craft, or discover.

Used at this layer, the chain does not alienate play. On the contrary, it gives players a kind of continuity they never had before: a sense of persistence, that what they build, earn, collect does not reset with every patch or sequel.

This is exactly the layer where I use blockchain in my games.

If you are curious and want to learn more, {{< extlink "https://www.youtube.com/watch?v=BPIWHTJ0FjQ" "catch the latest" >}} Cyberbrawl Grand Finals, try the game and join the next tournament.

Most of all, have fun! See you in the arena.

{{< youtube BPIWHTJ0FjQ >}}
*Cyberbrawl Grand Finals | Marlo vs Tarakanalada*

Thanks for reading! 