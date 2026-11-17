# tiny-chess-4k

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/fallingkuromaguro/tiny-chess-4k/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/fallingkuromaguro/tiny-chess-4k/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A complete chess engine in a single Python file of 3,989 bytes — standard library only. It plays through the environment API (`MAKEFUN_ENV_URL`, POST /game and /move), choosing from the legal moves the environment lists.

## Design

`main.py` is a compact loader around an LZMA-compressed engine. Inside: a 10×12 mailbox board with negamax search and alpha-beta pruning, iterative deepening under a fixed 60,000-node budget per move (no clock, fully deterministic), a transposition table, quiescence over captures and promotions, MVV-LVA and history ordering, two killer moves per ply, null-move pruning, late-move reductions, and material + piece-square evaluation with an endgame king table. Positions repeated from the game's move history score as draws, and any unexpected failure falls back to the environment's first legal move.

Move generation is verified against the published perft counts (start position, Kiwipete, and the standard test positions 3–5, colour-mirrored). On the kit's three practice trials it averages about 1,307 Elo.

## Run it

```sh
MAKEFUN_ENV_URL=<env-url> python3 main.py
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=szxhrrem&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)</sub>
