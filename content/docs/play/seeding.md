+++
title = "Tournament Bracket Seeding"
short = "Bracket seeding"
weight = 5
date = "2026-10-31"
tags = ["tournament", "bracket", "seeding"]
ShowToc = false
+++

Every Battle Nexus tournament is drawn by one published algorithm, with a commitment made before the draw, so neither the organizers nor the players can steer who meets whom.

Source: [github.com/FredericRezeau/cyberbrawl-bracket-seeding](https://github.com/FredericRezeau/cyberbrawl-bracket-seeding)  
Brackets: [nexus.cyberbrawl.io](https://nexus.cyberbrawl.io)

## Commit, then reveal

1. A secret salt is generated and its SHA-256 hash is published when the tournament is announced. That hash is the commitment: the salt is fixed before anyone has enlisted.
2. When registration closes, the seed is computed from the final roster and the salt.
3. The salt and the roster are revealed with the bracket, so anyone can recompute the seed and the first round.

## The draw

- Concatenate the player ids in enlistment order, append the salt, and take the SHA-256 of the string.
- The seed is the first four bytes of that hash, read as an integer.
- Shuffle the players with Fisher-Yates, driven by a linear congruential generator started from the seed.
- Pad the shuffled list with byes up to the next power of two.
- Pair the first half with the second: the player at `i` meets the player at `length / 2 + i`.

```
seedBracket(players, salt):
    seed = int(sha256(players.join('') + salt)[0:8], 16)
    rng  = s -> (s = (s * 9301 + 49297) mod 233280) / 233280, s = seed
    for i from players.length - 1 down to 1:
        j = floor(rng() * (i + 1))
        swap players[i], players[j]
    pad players with 'bye' up to the next power of two
    matches[i] = [players[i], players[length / 2 + i]]
```

## Verify a draw

Each event page on the Battle Nexus shows the hash, the salt, the seed and the roster, and a **Verify the draw** button that runs the algorithm in your browser and compares it with the bracket's first round. A player who withdrew after the draw stands in the bracket as a withdrawal seat; the check accepts that seat in their place.

The Legends tournaments played on Battlefy before the Battle Nexus were drawn there, so they carry no commitment to check.
