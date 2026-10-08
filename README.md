# theorycraft.cyberbrawl.io

Repo for [theorycraft.cyberbrawl.io](https://theorycraft.cyberbrawl.io).

The Cyberbrawl theorycraft website is where we document [Cyberbrawl](https://cyberbrawl.io)'s core mechanics from the shuffle and rating algorithms to technical deep dives and a public API for live game data.

Every page has an **Edit this page** link to its source here. Found a number that moved, a trick worth writing down, a build that works? Open a pull request.

## Layout

- `content/docs/` is the reference, the side menu. Four sections, `play`, `economy`, `onchain`, `data`, each a folder with an `_index.md` and its pages, ordered by `weight`. A page's `short` front matter is its name in the menu when the title is long.
- `content/posts/` is the talk: releases, deep dives, community write-ups, newest first.
- `content/authors/<handle>/_index.md` is a contributor card; posts name authors with `authors = ["handle"]`.
- `content/docs/data/api.md` is generated from the game server's routes. Do not edit it by hand, it is overwritten on the next generation.

## Quick start

```bash
hugo server -D
```

Serves on `http://localhost:1313` with drafts.

### A reference page

```bash
hugo new docs/play/your-page.md
```

```toml
+++
title = "Legend Rating"
short = "Legend Rating"  # the menu label, optional
weight = 3               # the order within the section
date = "2026-10-08"
description = "One line under the title."
tags = ["economy"]
ShowToc = true           # for long pages
+++
```

### A post

```bash
hugo new posts/your-post-slug.md
```

```toml
+++
title = "Post Title"
date = "2026-10-08T00:09:35+09:00"
slug = "your-post-slug"
draft = false
description = "One-liner summary"
tags = ["forge", "stellar"]
authors = ["kyungjin"]
authorDisplay = ["Fred Kyung-jin Rezeau"]
+++
```

Formatting, code, images, video and embeds are covered by the [cheat sheet](content/posts/cheat-sheet.md).

### A live card in a page

```
{{< card code="CARD00011" width="220px" >}}
{{< card code="CARD00040" still="true" >}}
```

Draws the card with the game's own script, animated unless `still`.

## Publish

```bash
hugo --gc --minify
```

Upload the contents of `public/` to the host.

## License

Content and code: see [LICENSE](LICENSE).
