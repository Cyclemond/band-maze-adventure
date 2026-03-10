# Band Maze Adventure — Project Memory

## What this is
A single-file HTML5 canvas web game built for Ian's young son Ellis.
Top-down maze game: navigate a character to find missing band instruments and return them to the band.

## Live URLs
- **Play:** https://cyclemond.github.io/band-maze-adventure/
- **Repo:** https://github.com/Cyclemond/band-maze-adventure
- **GitHub account:** Cyclemond

## Tech stack
- Pure HTML/CSS/JavaScript — no frameworks, no build step
- Single file: `index.html`
- Canvas 2D API for all rendering
- GitHub Pages for hosting (branch: `main`, path: `/`)

## Game structure
- **Scenes:** `menu` → `room` → `maze` → `win`
- **Room:** Band members on a purple stage, door on right wall leads to maze
- **Maze:** Recursive backtracker + braiding for loops; camera follows player
- **Win:** Confetti stars, happy dancing band, star rating if timed mode on

## Key state variables
| Variable | Purpose |
|---|---|
| `scene` | Current screen: menu / room / maze / win |
| `diff` | Difficulty: easy / medium / hard |
| `numMembers` | How many band members (1–4), chosen on menu |
| `timedMode` | Boolean — timed mode toggle |
| `totalStars` | Running star total across rounds (session only, no persistence) |
| `CELL` | Maze cell pixel size (auto-scaled per difficulty) |
| `mazeGrid` | 2D array: 1=wall, 0=path |

## Maze generation
- Recursive backtracker (perfect maze), then **braiding** removes dead ends to add loops
- Braid chance by difficulty: easy 55%, medium 35%, hard 18%
- Maze sizes: easy 13×11, medium 21×17, hard 31×25

## Band members & instruments (always in this order)
| Index | Name | Colour | Instrument |
|---|---|---|---|
| 0 | Roxy | Red | 🎸 Guitar |
| 1 | Bash | Purple | 🥁 Drums |
| 2 | Keys | Green | 🎹 Keyboard |
| 3 | Zippy | Orange | 🎺 Trumpet |

When `numMembers < 4`, only the first N entries are used everywhere.

## Maze colours
- **Walls:** `#1C1C24` (near-black charcoal) with `#2A2A38` top highlight
- **Paths:** `#C8A85C` / `#D4B870` (warm sandy gold checkerboard)
- High contrast by design — easy for kids to read

## Timed mode star thresholds
- ≤ 90 s (1.5 min) → ⭐⭐⭐
- ≤ 180 s (3 min)  → ⭐⭐
- > 180 s           → ⭐
- Timer colour: green → amber (90s) → red (180s)

## Controls
- **Keyboard:** Arrow keys or WASD; held key repeats at 130 ms intervals
- **Touch:** On-screen D-pad (bottom-right), shown during room + maze scenes
- **Menu taps:** difficulty buttons, band member count (1–4), timed toggle, start

## Design principles (keep these in mind)
- Target audience: 5-year-old child on an iPad
- Keep it fun and not frustrating — maze should be explorable, not punishing
- No audio (by design — keep it simple)
- No external dependencies
- All graphics drawn with canvas primitives (no images/sprites)
- D-pad buttons must be large enough for small fingers (72×72 px)

## Deployment
```bash
cd "/Users/ianbarton/Documents/Ellis band maze"
git add index.html
git commit -m "..."
git push   # auto-deploys to GitHub Pages
```
Pages can take ~1 minute to update after a push.
