# tiny-chess-01 entry

A chess engine in one Python file (`main.py`, LZMA-packed by the kit's
`makefun compress` from the readable source the agent sessions wrote).
It plays the gauntlet through the env at `MAKEFUN_ENV_URL`.

## Design

- 0x88 board, alpha-beta negamax with iterative deepening to a fixed
  node budget (60,000 nodes/move — never a clock, so replays match).
- Quiescence over captures (and all replies when in check), transposition
  table, MVV-LVA capture ordering, killer moves and history heuristic,
  null-move pruning.
- Evaluation: material plus formula piece-square terms (house-calibrated
  pawn advance, centre bonuses, king midgame/endgame tables with phase
  interpolation, bishop pair, king pawn-shield).
- Fully deterministic: no randomness, no wall clock, no model calls,
  Python 3.13 standard library only.

## Grade it locally

From the competition kit, with Docker:

    node cli/makefun.mjs grade-local --kit . --bot <this repo> --driver docker

Or run the env from the kit directly (see BUILD_LOG.md in the workspace)
and point `MAKEFUN_ENV_URL` at it.
