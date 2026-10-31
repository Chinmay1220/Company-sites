# chin-work — Brutalist explainers

Eleven explainer videos built with Claude on a free-only local toolkit: Kokoro TTS for
narration, Remotion for scenes, no API keys and no paid services anywhere in the chain.

Each project has its own dated folder holding `beat_sheet.json` (the source of truth —
narration, timing, scene routing and measured per-beat durations), a README, the signed
`PEDAGOGY.md` gate, the build script where one exists, the scene module, and a
`FRICTIONAL.md` process log.

**Master MP4s are not committed.** The eleven come to roughly 97 MB, and each reel
rebuilds from its beat sheet.

| Date | Project | Runtime | Beats |
|---|---|---:|---:|
| 2026-08-10 | [The Jobs Nobody Could Find](2026-08-10-jobs-nobody-could-find/) | 6:08 | 26 |
| 2026-08-11 | [Indexed or Invisible](2026-08-11-indexed-or-invisible/) | 10:52 | 42 |
| 2026-08-11 | [Shipped, Then Blocked](2026-08-11-shipped-then-blocked/) | 2:58 | 14 |
| 2026-09-09 | [The Test That Couldn't Fail](2026-09-09-the-test-that-couldnt-fail/) | 5:48 | 26 |
| 2026-09-09 | [Your Eval Is Lying to You](2026-09-09-your-eval-is-lying/) | 5:57 | 26 |
| 2026-09-21 | [The Variable That Vanished](2026-09-21-the-variable-that-vanished/) | 5:31 | 26 |
| 2026-09-25 | [The Test Where Everybody Got Zero](2026-09-25-everybody-got-zero/) | 4:01 | 22 |
| 2026-10-12 | [Finishing Your Sentences](2026-10-12-finishing-your-sentences/) | 4:17 | 21 |
| 2026-10-12 | [Static Into Pictures](2026-10-12-static-into-pictures/) | 4:16 | 23 |
| 2026-10-19 | [Teaching a Machine to Be Nice](2026-10-19-teaching-a-machine-to-be-nice/) | 5:05 | 22 |
| 2026-10-26 | [Practising In Its Sleep](2026-10-26-practising-in-its-sleep/) | 4:55 | 18 |

## Two strands

**Teardowns** check a notebook's own claims by re-running its code. Three found real
defects: an evaluation harness that scores correct answers zero and never called a model
at all; a causal model that adjusts away the exact effect its title asks about; a
synthetic-data report whose criterion moved between the run and the summary. Every figure
on screen is recomputed at build time from the notebook's own functions, under assertions
that fail the build rather than let the narration go stale.

**Kid-friendly cuts** carry the same material in plain words and cartoon metaphor —
diffusion, GPT, RLHF and world models — with no technical content softened into being
wrong. The animations compute the real thing where they can: the diffusion sprinkle
scenes run the actual forward equation, so the on-screen counter and the picture cannot
disagree.

## Frictional logs

Each folder's `FRICTIONAL.md` records what was tried and expected, where it resisted and
what was done next, what Claude contributed and what was accepted or changed, and what is
understood versus still open. They are deliberately unflattering — the silent renders that
wrote audio-only files, the unreadable three-second card, the inverted step mapping — on
the view that the failures are the part worth keeping.

## Rebuilding

```bash
python3 runtime/scripts/generate_audio_kokoro.py <reel>   # audio durations are the clock
python3 runtime/scripts/remotion_scenes.py     <reel>
python3 runtime/scripts/compile.py             <reel> --height 1080
```

Audio durations *are* the timeline, so any narration edit re-renders the beats it moves.
Verify every beat carries a video stream before compiling: a failed render can still write
an audio-only MP4 that the toolkit counts as a successful fill.
