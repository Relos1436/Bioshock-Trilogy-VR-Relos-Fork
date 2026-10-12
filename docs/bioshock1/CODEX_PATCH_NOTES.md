# Codex BioShock Remastered patch notes

This file records the local BioShock Remastered changes carried on the
`codex/bs1-wrench-visual-suppression` branch. The source baseline is upstream
v0.8.3, commit `41f004bc6a1e4fa8be0d0e0749f9ac5a0453e75e`.

## Changes and additions

- Physical wrench swing visual suppression: the VR hand pose stays pinned to a
  ready pose while the wrench's engine swing animation is active. The game's
  attack notification and separate wrench collision sampling path remain
  active, so damage is still resolved by the normal game path. An in-game
  `vrbones wrenchpose on|off|status` command provides an A/B switch.
- Wrench idle pose suppression: detect the exact `FidgetWrench` and
  `FidgetSlapWrench` clips through the weapon animation handle or the bounded
  SkeletonInstance animation map, then avoid adopting those evaluated poses for
  the VR hand. This removes the left-turning resting pose while leaving the
  animation channel running.
- Player-height calibration: add a `Player height correction (cm)` slider to
  the F10 VR camera panel and save it as `playerHeightCm` in `vrpreset.ini`.
  The correction moves the VR camera and controller/aim mapping base together;
  it does not move the game's pawn or collision capsule.
- Menu diagnostics and fallback key: F10 remains the primary overlay toggle;
  Insert also toggles it, with each key edge and resulting visibility written
  to the log.
- Engine research and runtime observations are recorded in
  `docs/bioshock1/ENGINE_NOTES.md`.

## User validation

The user reports that the swing suppression appeared to work in a headset test.
After the idle lookup follow-up, the user reports the wrench idle animation
appears fixed and that they could open the menu and adjust height. The user has
not separately confirmed hit registration in the latest build, so this note
does not claim that the latest idle follow-up revalidated hits.

## Build and installation record

The x86 `bioshockvr.dll` and `xinput1_3.dll` were installed under
`BioShock Remastered\\Build\\Final` on 2026-10-11. SHA-256:

- `bioshockvr.dll`: `EBC9B39DA247AE5BBCA4021EA237AB8BBBF9272FB32152DE75BE240DD028C6EE`
- `xinput1_3.dll`: `49D4F47BAE270D009CD95EBB08FA2D544A44CE393D4FA5213AA91FB9135F8061`

The user subsequently supplied the headset feedback above. These hashes identify
the installed build; they do not establish test coverage beyond that feedback.

— Codex
