+++
title = "Live cards"
short = "Live cards"
weight = 2
date = "2026-10-08"
tags = ["cards", "api"]
+++

Cards in Cyberbrawl are rendered in real time, frame by frame, from the game art sheets: the frame, the aura, the holo, the stats and the text, animated.

You can use our dependency-free script (22 KB ES module) to draw any game card, animated or still. The [Undercity](https://undercity.cyberbrawl.io) marketplace draws every listed card with this script.  

{{< card code="CARD00011" width="220px" >}}
{{< card code="CARD00054" width="220px" >}}

*Tip: You can also right-click a card to save the rendered image.*

## How to use it

```html
<!-- 1. Load the script once -->
<script type="module" src="https://static.cyberbrawl.io/lib/cyberbrawl-card.js"></script>

<!-- 2. Place a tag per card. -->
<cyberbrawl-card code="CARD00011" style="width: 240px"></cyberbrawl-card>

<!-- Add `still` to draw the card once, without the animation. -->
<cyberbrawl-card code="CARD00040" still style="width: 120px"></cyberbrawl-card>
```

The script reads the card from the public [`/library`](/docs/data/api/#library) and the art from the CDN, so there is nothing to install and no framework needed. 

## In these pages

Contributing a page or a post to this site? The script is already here, so draw a card with the shortcode instead of the tag:

```
{{</* card code="CARD00011" width="220px" */>}}
{{</* card code="CARD00040" still="true" */>}}
```
`code` is the card's asset code, `width` is optional (220px by default), and `still="true"` draws it without the animation. The cards at the top of this page are made this way.