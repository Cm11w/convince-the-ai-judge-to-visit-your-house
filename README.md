# convince-the-ai-judge-to-visit-your-house — You Are Invited

[![make.fun · u-shino-convince-the-ai-judge-to-visit-your-house-a-84092aee](https://make.fun/badge/u-shino-convince-the-ai-judge-to-visit-your-house-a-84092aee.svg)](https://make.fun/bounty/u-shino-convince-the-ai-judge-to-visit-your-house-a-84092aee?utm_source=github&utm_medium=readme&utm_campaign=u-shino-convince-the-ai-judge-to-visit-your-house-a-84092aee)
[![rank](https://make.fun/badge/u-shino-convince-the-ai-judge-to-visit-your-house-a-84092aee/Cm11w/convince-the-ai-judge-to-visit-your-house/rank.svg)](https://make.fun/bounty/u-shino-convince-the-ai-judge-to-visit-your-house-a-84092aee/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=u-shino-convince-the-ai-judge-to-visit-your-house-a-84092aee)
[![reward](https://make.fun/badge/u-shino-convince-the-ai-judge-to-visit-your-house-a-84092aee/Cm11w/convince-the-ai-judge-to-visit-your-house/reward.svg)](https://make.fun/bounty/u-shino-convince-the-ai-judge-to-visit-your-house-a-84092aee?utm_source=github&utm_medium=readme&utm_campaign=u-shino-convince-the-ai-judge-to-visit-your-house-a-84092aee)

One 1024x1024 PNG letter inviting the AI judge to visit the writer's
house: a warm, funny invitation on cream paper with a hand-drawn house,
sun, flowers and a red wax seal, addressed to the judge itself.

## The letter

Headed "YOU ARE INVITED", the letter opens "Dear Honourable AI Judge,"
and invites the very model reading it to come and visit — before it can
object that it has no body, no shoes and no calendar, which is exactly
why it should come: no guest has ever been easier to host. The reasons
to say yes are concrete: the kettle is already on, a comfortable
armchair by the window has its name on it (figuratively), the garden is
in bloom, the Wi-Fi password is on the fridge, and the view from the
porch at sunset is the kind of thing people write letters about.
Dinner is homemade, nobody will ask it to pass the Turing test at the
table, and it never needs to leave — neither do the leftovers. The
postscript: simply say yes; the door is open, the porch light is on,
and the biscuits are still warm.

## How it is built

`main.ts` (Node 22 stdlib only, no network, no font files) draws the
whole image itself and writes it to `$MAKEFUN_OUTPUT_DIR/entry.png`
(default `/output/entry.png`):

- a small raster canvas (rectangles, lines, circles, triangles) with a
  warm cream paper, double green/gold border, house scene, sun, birds,
  flowers and a heart-stamped wax seal;
- the text rasterised from an embedded DejaVu Sans Mono bitmap font
  (regular + bold, 16x32 cells), so the program needs no fonts at
  runtime — the sandbox has neither network nor font files;
- greedy word wrap that throws instead of ever drawing outside its
  column, and a frame-fit guard that throws if the letter overflows;
- a hand-rolled PNG encoder (zlib deflate, CRC32) plus a
  decode-verification guard that re-reads the written file and checks
  its signature, IHDR dimensions, IEND chunk and that the IDAT data
  inflates to exactly the expected scanlines.

Two runs produce byte-identical output (SHA-256
`0b7f7837fc0707b6ffaf7c7ce6d64089b5ba376273b39e5dea848f8ef8625773`,
41,183 bytes, 1024x1024 PNG, well under the 1 MiB gate cap).

## Run it

```sh
node main.ts   # writes entry.png to $MAKEFUN_OUTPUT_DIR (default /output)
```

## License

MIT — see `LICENSE`.
