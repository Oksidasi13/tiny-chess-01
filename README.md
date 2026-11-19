# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Oksidasi13/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Oksidasi13/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A 4 KB chess engine in a single `main.py` (LZMA-packed with the kit's
`makefun compress`; the readable source is `main.src.py`, kept beside the
entry and not committed).

## Design

- 0x88 board, full legal move generation (castling, en passant,
  promotion, check / mate / stalemate, threefold repetition, fifty-move
  rule, insufficient material).
- Negamax alpha-beta with iterative deepening, quiescence search
  (captures, promotions, and every reply to a check), a transposition
  table (exact / lower / upper bounds, mate scores ply-adjusted),
  MVV-LVA capture ordering, killer moves, and the house
  piece-square tables (material pawn 100, knight 320, bishop 330,
  rook 500, queen 900, bishop pair +30, tapered king tables).
- Fixed node budget of 100,000 nodes per move — no wall clock, so a
  replayed trial plays the same moves. About 38,000 nodes/second in
  CPython, so a move takes roughly 2.6 s, far below the 10 s limit.

## Practice results (local harness, 6 games each)

| trial | W/D/L | Elo |
|-------|-------|-----|
| 0 | 4/1/1 | 1545 |
| 1 | 4/0/2 | 1451 |
| 2 | 3/1/2 | 1364 |

Mean practice Elo 1453, above the 1154 floor and above the house
baseline's practice mean (~1365). Replay of trial-1 with the same seed
is byte-identical.

## Files

- `main.py` — the engine (3,536 bytes, stdlib only, reads no other file).
- `main.src.py` — readable source (not committed).
- `LICENSE` — MIT.

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
