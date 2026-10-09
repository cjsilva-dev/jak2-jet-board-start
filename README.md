# JET-Board Start — Jak II

**The JET-Board from the first moment of the game.** An [OpenGOAL](https://opengoal.dev) mod for
*Jak II* that puts Keira's JET-Board in Jak's hands from the prison onwards. Press **R2** anywhere the
game lets you ride, from the Fortress escape through all of Haven City and beyond, instead of waiting
for the Stadium missions.

## What changes

- Jak always has the JET-Board. It is granted every frame, so a new game, a loaded save, or the story
  handing it back can't take it away.
- The story still plays out as written. Keira's training (*Win JET-Board Stadium Challenge*) works as
  before: the board on the stand, the training, the judges. Afterwards, the one scene where Jak puts
  the board back on its stand plays once, because the next mission waits for it, and then never again.
  Jak keeps the board; later, Samos still hands it over for the Haven Forest scouts, which changes
  nothing.
- Everything else is the stock game: where the board is allowed, how it rides, the tricks, the
  Stadium challenges and the board missions.

Nothing is required of the player. There are no settings.

## How it is done

Two small changes in `goal_src/jak2/`:

- `engine/mods/mod-custom-code.gc` — `runs-every-frame` sets the `board` game feature.
- `engine/util/script.gc` — the `game-feature?` script form, which the Stadium's region script uses to
  decide whether to play the "put the JET-Board back" scene, answers *no* once that scene has run
  (the `stadium-board1-done` task node is closed). Without this the scene would replay on every visit
  to the Stadium until the Haven Forest mission.

The game's own task logic (`add-board` / `sub-board`) is untouched; the every-frame grant simply
outlasts it.

## Not included

This mod contains only code. Everything it shows comes from your own copy of *Jak II*. HD texture
packs are not part of it; install your favourite pack through the OpenGOAL launcher as usual.

## Credits

- Built on the [OG-Mod-Base](https://github.com/OpenGOAL-Mods/OG-Mod-Base) template and the
  [OpenGOAL](https://github.com/open-goal/jak-project) project.
- *Jak II* © Naughty Dog / Sony Interactive Entertainment. This is a fan project.

The mod base's own readme (with OpenGOAL setup links) is kept in [README.opengoal.md](README.opengoal.md).
