+++
title = "REST API"
short = "REST API"
weight = 1
date = "2026-10-08"
tags = ["api", "data"]
ShowToc = false
+++

Base URL: `https://connect.cyberbrawl.io`

All endpoints below are public, `GET`, and answer JSON. Amounts are strings (seven decimals), unless noted. Card ids are the library's (`card_02_00011`); the matching onchain asset code is `CARD` plus the five digits (`CARD00011`), issued by `GBAKUWF2HTJ325PH6VATZQ3UNTK2AGTATR43U52WQCYJ25JNSCF5OFUN`.

---

## Library
Get the list of all cards currently available in the game. Optional `lang` for localized names.

**URL**: `https://connect.cyberbrawl.io/library`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
{
  "card_01_00001": {
    "id": "card_01_00001",
    "type": 1,
    "name": "Overload I",
    "stats": [2, 0, 0, 0],
    "boost": 0,
    "desc": ""
  },
  "card_02_00012": {
    "id": "card_02_00012",
    "type": 2,
    "name": "Card Name",
    "stats": [0, 4, 0, 0],
    "boost": 0,
    "desc": "Card description"
  }
}
```

---

## Unlocks
Get the ranked ladder with the card unlocked at each step, and the exclusive cards that are never unlocked by rank. Optional `lang` for localized names.

**URL**: `https://connect.cyberbrawl.io/unlocks`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
{
  "ladder": [
    {
      "stars": 0,
      "rank": "Recruit",
      "card": {
        "id": "card_02_00030",
        "type": 4,
        "name": "Hellfire\nDroid",
        "stats": [0, 0, 0, 0],
        "boost": 0,
        "group": "droid",
        "passive": true,
        "desc": "Deal +1 Damage on your turn. Passive."
      }
    }
  ],
  "exclusive": [
    {
      "id": "card_02_00040",
      "type": 6,
      "name": "Blood\nPact",
      "stats": [0, 6, 0, 0],
      "boost": 0,
      "desc": ""
    }
  ]
}
```

---

## Player
Get player profile and stats

**URL**: `https://connect.cyberbrawl.io/player?id={playerId}`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
{
  "id": "kyungjin",
  "name": "Kyungjin",
  "back": 8,
  "stats": [125, 1323800, 64, 0, 29, 5428, 7869, 60],
  "badges": {
    "legend": true,
    "elite": false,
    "dev": true
  }
}
```

---

## Leaderboard
Get leaderboard rankings. Only the live boards are served: the current season (`season:{index}`), today (`daily:{YYYY-MM-DD}`), and the final alpha standings (`alpha`).

**URL**: `https://connect.cyberbrawl.io/server/leaderboard?name={name}`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
[
  {
    "id": "ihgux3",
    "name": "Pipay",
    "back": 10,
    "stats": [125, 1246575, 59, 2, 56, 30685, 40002, 11520],
    "score": 4194
  }
]
```

---

## Server Stats
Get overall game statistics.

**URL**: `https://connect.cyberbrawl.io/server/stats`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
{
  "credit": {
    "supply": 299792458,
    "earned": 22070571.68711
  },
  "players": {
    "total": 160567
  },
  "battles": {
    "total": 6287446
  }
}
```

---

## Meta
Get the ranked meta: a summary of the last 2,000 ranked battles, a live feed, archetypes with their share, win rate and trend, the matchup table, the cards table, the common decks, the ladder and the deck shapes. Large, refreshed every minute.

**URL**: `https://connect.cyberbrawl.io/server/meta`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example** (abridged):
```json
{
  "time": 1791431613764,
  "summary": { "total": 184866, "battles": 2000, "firstWinRate": 58.1, "turns": 9.7, "seconds": 75 },
  "feed": [
    { "t": 1791431609718, "turns": 9, "win": 0, "ranks": ["Veteran III", "Veteran III"], "archetypes": ["Hellfire Spec · Hellfire Mastery", "No Spec · Overload Mastery"] }
  ],
  "archetypes": [
    { "key": "card_02_00050|card_02_00019", "label": "Hellfire Spec · Hellfire Mastery", "games": 2005, "share": 50.1, "winRate": 53.8, "turns": 7.4, "trend": -10.3, "cards": ["card_02_00019", "card_02_00050"] }
  ],
  "matchups": { "keys": ["…"], "rows": [["…"]] },
  "cards": [], "decks": [], "ladder": [], "earnings": {}, "pool": {}
}
```

---

## Battle Replays
Get recent battle replay data: the last 100 battles, newest last. Replays expire a day after the battle; `expire` is the Unix time in milliseconds when a replay leaves the list. With `id={replayId}` the full replay (the battle and its turn states) is returned instead, as the game plays it back.

**URL**: `https://connect.cyberbrawl.io/battles/replay`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
{
  "result": [
    {
      "id": "p87ajw",
      "expire": 1791517633000,
      "turns": 10,
      "players": [
        {"name": "Jieun", "id": "jieun", "winner": true},
        {"name": "Kyungjin", "id": "kyungjin", "winner": false}
      ]
    }
  ]
}
```

---

## Tournaments
Get the Battle Nexus: the live tournament and its brackets, rounds, matches with scores and the replay ids of their battles, and the registered players.

**URL**: `https://connect.cyberbrawl.io/battles/nexus`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example** (abridged):
```json
{
  "live": { "id": "beta-launch", "title": "legends-tournament", "cover": "/assets/aae6cb-poster_0002.png", "enabled": false, "time": 1734429298, "registrations": true },
  "brackets": [
    {
      "id": "beta-launch",
      "rounds": [
        { "id": "round-32", "current": false, "matches": [ { "bestof": 9, "players": ["6pqirj", "eesphk"], "score": [5, 3], "battles": ["3c6lt3", "y9nrqr"] } ] }
      ],
      "players": [ { "id": "gonz0", "name": "gonz0", "back": 2, "stats": [] } ]
    }
  ]
}
```

---

## Market Prices
Get the market quotes of every game asset in every supported currency, as found on the Stellar DEX by path. `ask` is the best price to buy one unit now, `bid` the best price to sell one now, each with the path of hops the trade goes through (empty for a direct order). `prices` is empty when no path exists. With `extended=1` every card of the game is listed, with `prices: null` for those never offered. Currencies: `XLM` (`native`), `USDC`, `CREDIT`, `KALE`.

**URL**: `https://connect.cyberbrawl.io/listings/prices?extended=1`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
[
  {
    "asset": { "code": "CARD00011", "issuer": "GBAKUWF2HTJ325PH6VATZQ3UNTK2AGTATR43U52WQCYJ25JNSCF5OFUN", "meta": { "id": "card_02_00011", "type": 4, "name": "Tactical\nHeal", "stats": [2, 2, 0, 0], "boost": 0, "desc": "" } },
    "market": { "code": "XLM", "issuer": "native" },
    "prices": {
      "ask": { "price": "25.0000000", "path": [] }
    },
    "updated": "2026-10-08T03:52:37.435Z"
  }
]
```

### One asset
The quotes of one asset in every currency, refreshed on demand.

**URL**: `https://connect.cyberbrawl.io/listings/price?code={code}&issuer={issuer}`  
**Method**: `GET`  
**Auth required**: No

```json
{
  "asset": { "code": "CARD00011", "issuer": "GBAKUWF2HTJ325PH6VATZQ3UNTK2AGTATR43U52WQCYJ25JNSCF5OFUN" },
  "prices": [
    { "market": { "code": "XLM", "issuer": "native" }, "prices": { "ask": { "price": "25.0000000", "path": [] } }, "updated": "2026-10-08T03:52:37.435Z" },
    { "market": { "code": "CREDIT", "issuer": "GBAKUWF2HTJ325PH6VATZQ3UNTK2AGTATR43U52WQCYJ25JNSCF5OFUN" }, "prices": { "ask": { "price": "158573.2657562", "path": [ { "asset_type": "credit_alphanum12", "asset_code": "LIBRE", "asset_issuer": "GAYCC…" }, { "asset_type": "native" } ] } }, "updated": "2026-10-08T03:53:46.955Z" }
  ]
}
```

---

## In-game Market
Every collectible card with its best ask and bid on the in-game market, where cards trade for CREDIT between accounts and the game server settles the trade. `asks` and `bids` are the number of open orders on the card, `last` the last sale. `fee` is the share of a sale taken by the game.

**URL**: `https://connect.cyberbrawl.io/market/book`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
{
  "fee": 0.05,
  "rows": [
    {
      "card": "card_02_00042",
      "ask": 120,
      "bid": 95.5,
      "asks": 2,
      "bids": 1,
      "updated": 1791985731355,
      "last": { "price": 110, "at": 1791900000000 }
    }
  ]
}
```

---

## Sui Market
Every card listed for sale on Sui, cheapest first, from the game's index of Kiosk listings. `price` is in MIST (1 SUI = 1,000,000,000 MIST). `royalty` is what the transfer policy takes on a sale, in basis points, with a minimum in MIST.

**URL**: `https://connect.cyberbrawl.io/sui/market`
**Method**: `GET`
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
{
  "network": "mainnet",
  "listings": [
    { "item": "0xdd95…ed19", "kiosk": "0x8241…32e6", "card": "card_02_00031", "code": "CARD00031", "name": "Primal\nOverload", "type": 6, "price": "50000000000", "seller": "0xca54…732e", "at": 1791785882342 }
  ],
  "royalty": { "bps": 500, "min": "0" }
}
```

---

## Sui Cards
The cards a Sui address holds, in its wallet and in the kiosks it owns.

**URL**: `https://connect.cyberbrawl.io/sui/cards?address={address}`
**Method**: `GET`
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
{
  "network": "mainnet",
  "cards": [
    { "id": "card_02_00031", "object": "0xdd95…ed19", "kiosk": "0x8241…32e6", "cap": "0xde78…9b7e", "listed": true, "exclusive": false },
    { "id": "card_02_00072", "object": "0xb4a6…2416" }
  ],
  "kiosks": [
    { "kiosk": "0x8241…32e6", "profits": "0" }
  ]
}
```

---

## Forge Price
Get what the ION Forge charges today and the rules the contract applies. `base` is CREDIT per ION stroop in basis points (the contract's unit), `ion` the same as CREDIT per ION; `premium` is the 24-entry table of the power premium in basis points, `duration` the seconds of a forge at power 1; `fee` is the in-game service fee. `contract` is the Forge contract on Stellar mainnet; its source and the cost formulas are at https://github.com/litemint/cyberbrawl-contracts.

**URL**: `https://connect.cyberbrawl.io/forge/price`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
{
  "contract": "CDJZCLXBQ6QRRQIPOV73HXOL5HWZBDUWHRESMD23PORSFAGZD3ELZQMH",
  "base": 242547,
  "ion": 24.254684684684683,
  "premium": [10000, 12708, 14620, 16148, 17443, 18578, 19595, 20520, 21373, 22166, 22908, 23608, 24270, 24900, 25501, 26076, 26629, 27160, 27673, 28168, 28647, 29111, 29562, 30000],
  "duration": 172800,
  "fee": { "fixed": 50, "percent": 2.5 }
}
```

---

## Armory

Get a player's standing, badges and collection.

**URL**: `https://connect.cyberbrawl.io/armory/data/{playerId}`  
**Method**: `GET`  
**Auth required**: No

```json
{
  "id": "kyungjin",
  "name": "Kyungjin",
  "back": 6,
  "badge": 3,
  "badges": [ { "id": 0, "name": "Trailblazer", "earned": true } ],
  "stars": 120,
  "rank": "Legend",
  "high": "Legend",
  "legend": 4,
  "rating": 1815,
  "season": 1,
  "streak": 1,
  "bestStreak": 12,
  "wins": 5428,
  "xp": 1323800,
  "achievementPoints": 60,
  "owned": ["card_02_00011"],
  "unlocks": { "ladder": [], "exclusive": [] },
  "ladder": { "starsPerRank": 5, "legend": 120, "fullLegend": 125 }
}
```

### Search
Players by name, Battle ID or wallet, up to ten, with their standing.

**URL**: `https://connect.cyberbrawl.io/armory/search?q={text}`  
**Method**: `GET`  
**Auth required**: No

```json
[
  { "id": "kyungjin", "name": "Kyungjin", "back": 6, "badge": 3, "rank": "Legend", "stars": 0, "legend": true }
]
```

---

## Events
The current in-game events, as the game's journal shows them.

**URL**: `https://connect.cyberbrawl.io/events`  
**Method**: `GET`  
**Auth required**: No

```json
{
  "id": "7c2e91a4-b3f5",
  "list": [
    { "id": "e5d0a7c2-41f8", "cover": "/assets/aae6cb-poster_0003.png", "title": "Hero Protocol", "titleColor": "#8470ec", "desc": "One Hero at your side, one power per battle.", "sequence": "iris" }
  ]
}
```

---

## Achievements
The list of achievements and their points.

**URL**: `https://connect.cyberbrawl.io/achievements`  
**Method**: `GET`  
**Auth required**: No

---

## Badges
Get the list of available player badges.

**URL**: `https://connect.cyberbrawl.io/badges`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
[
  {"id": 0, "name": "Trailblazer", "property": "trailblazer"},
  {"id": 1, "name": "Champion", "property": "elite"},
  {"id": 2, "name": "Legend", "property": "legend"}
]
```

---

## Heroes
Get the list of available heroes.

**URL**: `https://connect.cyberbrawl.io/heroes`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
[
  { "id": 1, "key": "hero00001", "name": "Kismet", "title": "The Dealer", "power": "Mulligan", "tier": 4, "price": 100, "desc": "Discard a random card and draw next. Once per battle." },
  { "id": 3, "key": "hero00003", "unlock": { "quest": "r1:overclock" }, "hint": "Complete the Overclock Heat quest.", "name": "Ohm", "title": "The Technician", "power": "Failsafe", "tier": 5, "price": 200, "desc": "All cards in your hand get +50% Overclock chance this turn. Once per battle." }
]
```

---

## Card Backs
Get the list of available card backs.

**URL**: `https://connect.cyberbrawl.io/cardbacks`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
[
  {"id": 0, "name": "Cyber Brawl", "desc": "Cyber Brawl Logo"},
  {"id": 1, "name": "Red Dragon", "desc": "By Prasong Tadoungsorn"},
  {"id": 5, "name": "Insignia", "desc": "Show off your rank!"}
]
```

---

## Community
Get community content and featured videos.

**URL**: `https://connect.cyberbrawl.io/server/community`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
{
  "links": [
    {
      "id": "link-eb34e83d-wow1-0",
      "author": "Fred Kyung-jin Rezeau",
      "desc": "CyberBrawl Dev",
      "link": "https://www.youtube.com/watch?v=xLkj-wEfvsg",
      "image": "https://img.youtube.com/vi/xLkj-wEfvsg/hqdefault.jpg"
    }
  ]
}
```
