+++
title = "Ladder and ranks"
short = "Ladder and ranks"
weight = 2
date = "2026-10-08"
tags = ["ranked", "ladder"]
+++

Ranked play is a ladder of stars. A win earns a star, a loss costs one, and every five stars is a rank. There are twenty-five ranks, from Recruit to Legend, so the climb to Legend is 120 stars.

## The ranks

| # | Rank | Stars to enter |
|---|---|---|
| 1 | Recruit | 0 |
| 2 – 4 | Adept I, II, III | 5, 10, 15 |
| 5 – 7 | Soldier I, II, III | 20, 25, 30 |
| 8 – 10 | Veteran I, II, III | 35, 40, 45 |
| 11 – 13 | Elite I, II, III | 50, 55, 60 |
| 14 – 16 | Champion I, II, III | 65, 70, 75 |
| 17 – 19 | Commander I, II, III | 80, 85, 90 |
| 20 | Warlord | 95 |
| 21 | High Warlord | 100 |
| 22 | Master | 105 |
| 23 | Grandmaster | 110 |
| 24 | Hero | 115 |
| 25 | Legend | 120 |

Each rank unlocks a card for your collection, and the unlocks are listed with the ladder on [cards.cyberbrawl.io](https://cards.cyberbrawl.io). The same data is served by the API as [`/unlocks`](/docs/data/api/#unlocks).

## Legend

At 120 stars the stars stop counting. Legends are ordered by rating instead, a number that moves with every ranked battle against other players, and the season board at [armory.cyberbrawl.io](https://armory.cyberbrawl.io) shows the top of it. A player's page in the Armory shows the rank, the stars inside it, and for a Legend the position and the rating.

Reaching Warlord in any season earns the Forgemaster badge, which opens the [Forge](/docs/economy/forge/).

Live standings: [`/server/leaderboard?name=season:{index}`](/docs/data/api/#leaderboard).
