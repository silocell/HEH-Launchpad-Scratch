# Scratch Games

Six games built in Scratch, packaged so they run straight in a browser —
no Scratch account, no sign-in, nothing to install. They're the arcade
half of [Homework Launchpad](https://github.com/silocell/HEH-Homework),
a homework site built for a Year 7 class, and they live in their own repo
because 12 MB of packaged games doesn't belong in a repo you push to
several times a day.

**Play them:** open `index.html`, or visit the published site.

---

## The games

| Game | What it is |
|---|---|
| **VroomZoom Car Simulator** | A real circuit — three laps, hidden checkpoints, and the grass slows you down. W/↑ to go, A/D or ←/→ to steer. |
| **The Maze of Confusion** | Three freshly generated neon mazes, sixty seconds for all of them. The walls stop you; the clock is what beats you. |
| **Ducks Rampage** | Dodge the angry yellow ducks, catch the silver ones. Three hearts. |
| **Fruit Slash** | Swipe to slice the fruit, never the bomb. Three lives, and it speeds up as you score. |
| **Gem Quest** | A small RPG — walk the meadow, spin your sword at the slimes, bring home all three gems. |
| **2 Player Pong** | Two players on one keyboard: ←/→ against W/S, spin off the paddles, first to 7. |

## How they're put together

Each `sg-*.html` is a self-contained page produced by the
[TurboWarp Packager](https://packager.turbowarp.org/): the Scratch project
and the runtime that plays it are both inlined, so the file works offline
and from any folder. That's why they're around 2 MB each.

`game-hud.js` is the one piece written by hand. Scratch draws its variable
readouts *on* the stage, where they sit on top of the game — on the maze
they covered the walls. So every game hides Scratch's own boxes and this
file redraws the few that matter in a strip above the stage, along with
the close button. A page declares what it wants before loading it:

```js
window.GameHUD = { title: "2 Player Pong",
                   chips: [ {label: "Player 1", v: "Player 1 Score"} ] };
```

where `v` is the name of a variable on the Scratch stage.

## Why packaged rather than embedded

Scratch's own embed needs scratch.mit.edu to be reachable and loads a
player wrapped in Scratch's chrome. School networks block plenty, and the
site had to work on Chromebooks with nothing installed. A packaged page
has no outside dependency at all: if the page loads, the game runs.

## Licence

The games and `game-hud.js` are released under the
[GNU GPL v3](https://www.gnu.org/licenses/gpl-3.0.html) — see `LICENSE`.

Each packaged page also contains the Scratch VM and TurboWarp's runtime,
which are the work of the Scratch Foundation and the TurboWarp project and
carry their own licences. The GPL here covers the games, not that
bundled runtime.
