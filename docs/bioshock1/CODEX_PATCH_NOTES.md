# Codex BioShock Remastered patch notes

This file records the local BioShock Remastered changes carried on the
`codex/bs1-wrench-visual-suppression` branch. The source baseline is upstream
v0.8.3, commit `41f004bc6a1e4fa8be0d0e0749f9ac5a0453e75e`.

The upstream-connected public fork is
https://github.com/Relos1436/Bioshock-Trilogy-VR-Relos-Fork. A private
standalone backup with the same changes and upstream history is at
https://github.com/Relos1436/bioshock-trilogy-vr-private. GitHub does not permit
a public repository to have a private fork, so the backup is not connected to
the upstream fork network.

- Public fork renamed on 2026-10-12 from `bioshock-trilogy-vr` to
  `Bioshock-Trilogy-VR-Relos-Fork`. — Codex

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

## Requested VR features — 2026-10-12

- Added independent tracking for the controller not currently driving the
  equipped holdable. It uses that hand's own XR pose and saved model offsets;
  the weapon attachment remains parked when the right hand is the off hand.
  This does not include two-handed grip.
- Added an in-game hands-menu toggle for off-hand tracking and saved it in
  `hands.ini`.
- Added visual recoil for supported gun classes and OpenXR haptics for gun
  fire, plasmid casts, wrench attacks, and calibration success. Recoil changes
  the rendered viewmodel pose only; it does not change the controller aim ray
  or game damage logic. The recoil toggle and strength control are in the
  hands menu.
- Added left/plasmid-hand aim calibration and an aim-dot toggle for plasmids.
  Calibration and dot preference are stored in `aim_plasmid.ini` in the mod's
  data directory.
- Feature attribution and the MIT license notice for the implementation
  reference are in `THIRD_PARTY_NOTICES.md`.
- Build status: all CMake Release targets compiled with Visual Studio 2026's
  x86 toolchain. CMake's normal compiler probe failed with `C1902` in its
  dependency wrapper, so the configure used the x86 compiler and explicitly
  forced the CMake ABI probe; `dumpbin` verified the resulting DLL is PE32,
  machine `0x014C` (x86). This is compile evidence only; no headset behavior
  has been verified for these new features.

— Codex

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
