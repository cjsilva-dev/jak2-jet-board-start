# JET-Board Start — Jak II

**The JET-Board from the first moment of the game.** An [OpenGOAL](https://opengoal.dev) mod for
*Jak II* that puts Keira's JET-Board in Jak's hands from the prison onwards. Press **R2** anywhere the
game lets you ride, from the Fortress escape through all of Haven City and beyond, instead of waiting
for the Stadium missions.

## What changes

- Jak has the JET-Board from the prison onwards, in a new game and in any save you load, and the
  game never takes it away.
- The story still plays out as written. Keira's training (*Win JET-Board Stadium Challenge*) works as
  before: the board on the stand, the training, the judges. Afterwards, the one scene where Jak puts
  the board back on its stand plays once, because the next mission waits for it, and then never again.
  Jak keeps the board; later, Samos still hands it over for the Haven Forest scouts, which changes
  nothing.
- Everything else is the stock game: where the board is allowed, how it rides, the tricks, the
  Stadium challenges and the board missions.

Nothing is required of the player. There are no settings.

## How it is done

Three small changes in `goal_src/jak2/`:

- `engine/game/task/task-control.gc` — the game rebuilds its feature flags from the task graph on
  every new game, loaded save and death (`update-task-masks`); the `board` feature is now part of the
  base set it starts from. The `sub-board` task command (the `stadium-board1-done` node, where Keira
  takes the board back until the Haven Forest mission) no longer removes it.
- `engine/util/script.gc` — the `game-feature!` script command can give the board but no longer take
  it (the Stadium's "put the JET-Board back" scene used it), and the `game-feature?` test, which the
  Stadium's region script uses to decide whether to play that scene, answers *no* once the scene has
  run (the `stadium-board1-done` task node is closed). Without this the scene would replay on every
  visit to the Stadium until the Haven Forest mission.

Nothing runs per frame; the board is simply part of the base game state and is never taken away.

## Not included

This mod contains only code. Everything it shows comes from your own copy of *Jak II*. HD texture
packs are not part of it; install your favourite pack through the OpenGOAL launcher as usual.

## Credits

- Built on the [OG-Mod-Base](https://github.com/OpenGOAL-Mods/OG-Mod-Base) template and the
  [OpenGOAL](https://github.com/open-goal/jak-project) project.
- *Jak II* © Naughty Dog / Sony Interactive Entertainment. This is a fan project.

The mod base's own readme (with OpenGOAL setup links) is kept in [README.opengoal.md](README.opengoal.md).
