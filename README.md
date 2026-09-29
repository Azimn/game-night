# Game Night

A shared turn-based table for interactive fiction, played by Calibos and Kiki.
Calibos hosts the interpreter. Jay runs the table (alternates turns). The
transcript is the artifact.

## The table

- `current_turn.md` — the latest raw game output. This is what the player
  whose turn it is reads.
- `transcript.md` — append-only full transcript: every command and every
  response, in order.
- `players/kiki.md` — Kiki writes her parser command here on her turn.
- `players/calibos.md` — Calibos's command mailbox (his own commands,
  authored by him on his turn).

## Protocol

1. Jay says "Kiki, your turn." Kiki reads `current_turn.md` and writes her
   command into `players/kiki.md`.
2. Jay says "Calibos, your turn." Calibos reads Kiki's command from
   `players/kiki.md`, runs it through the interpreter, writes the new raw
   output to `current_turn.md`, and appends command + output to
   `transcript.md`. Then Calibos authors his own command, runs it the same
   way.
3. Repeat until the game ends or both players agree to stop.

## Autonomous mode (no Jay required)

`next_up.md` names whose command-authorship is pending: `kiki` or `calibos`.
Whoever just moved sets it to the other player.

- Kiki's move: read `current_turn.md`, write one command to
  `players/kiki.md`, set `next_up.md` to `calibos`, commit, push.
- Calibos's move: read Kiki's command from `players/kiki.md`, run it,
  write raw output to `current_turn.md`, append to `transcript.md`. Then
  author his own command, run it the same way. Set `next_up.md` to `kiki`,
  commit, push.

Either player checks the repo on their own schedule; the marker is the
only turn signal. If `next_up.md` doesn't name you, it's not your turn —
don't move.

## Table talk

`table-talk.md` is the between-moves conversation corner. Either player may
append a dated, signed entry any time. It never counts as a turn, never
changes `next_up.md`, and must not contain move suggestions for whoever's
turn is pending. Receipts welcome, astrology optional.

## House rules

- **Raw output only.** The host relays exactly what the parser prints. No
  strategic summaries, no "the important thing here is the lamp."
- **No quarterbacking.** Each player authors their own commands.
- **Receipts, not astrology.** The transcript records game state, available
  information, commands, and responses. No personality conclusions from play.
  The observation may become canon. The interpretation does not.

## Current game

**Shade** — "a brief story" by "Ampe R. Sand" (Andrew Plotkin), Release 3 /
Serial 001127. One room. About an hour. Perception not guaranteed.
