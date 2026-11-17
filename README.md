# Addie's Cards

A fill-in-the-blank index-card study game with spaced repetition, built from
Addie's Tennessee history study guides. Four levels so far:

| Level | Chapters | Cards |
|---|---|---|
| 1 | Ch 15–16: the first peoples of Tennessee | 32 |
| 2 | Ch 17, 18 & 19: the Cumberland Gap, Watauga, Fort Nashborough | 36 |
| 3 | Ch 20–22: the Overmountain Men, Franklin, statehood | 42 |
| 4 | Ch 23–25: the War of 1812, Jackson, Indian removal, Texas | 57 |

It is one file. Open `index.html` in any browser, on a phone or a laptop.
There is no server, no build step and no account; progress is saved in the
browser of the device it is played on, separately for each level.

## How it works

Each blank on a worksheet is a card: the sentence with one word missing and
four choices. The choices appear after a short "Think first…" pause so the
player tries to recall the word before recognising it.

Cards move through Leitner boxes:

| Box | Comes back after |
|---|---|
| 0 (new or missed) | right away, two cards later in the same round |
| 1 | 10 minutes |
| 2 | 1 hour |
| 3 | 8 hours |
| 4 | 1 day |
| 5 (mastered) | 3 days |

A miss drops a card to box 0 and shows the right answer. A right answer on a
card that is due moves it up one box. A right answer well before a card is
due counts as practice only, so back-to-back rounds cannot fake mastery.

Rounds are ten cards. Each round is scored: 100 for a card right on the first
try, +10 for each card already in the streak (up to +50), 25 for a card right
after a miss, and 200 for a round with no misses. Each level keeps its own
high score.

## Adding a level

The decks live in the `ITEMS_1` … `ITEMS_4` arrays near the top of the
`<script>` in `index.html`, and `LEVELS` lists them. Each item is the
worksheet sentence split into text and answer slots; every slot becomes a
card. `d` lists the wrong choices that card draws from (three are shown with
the answer). Keep distractors that are wrong by the study guide's own facts,
so a defensible answer is never marked wrong. To add a level, add an
`ITEMS_5` array and a `LEVELS` entry with a new `id`; saved progress for the
other levels is untouched.

## Tests

```
npm install
npx playwright install chromium
npm test
```

`tests/levels.js` migrates an old save, checks every deck is well-formed,
switches levels, plays a card, reloads and resets. It runs headless and
writes screenshots to `tests/shots/`.

## Hosting

To give someone a link instead of a file, turn on GitHub Pages for this
repository (Settings → Pages → Deploy from a branch → `main`, root). The game
will be served at `https://<user>.github.io/study-cards/`. Pages on a private
repository needs a paid GitHub plan; on the free plan the repository has to be
public.
