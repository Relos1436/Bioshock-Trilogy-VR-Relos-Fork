# Third-party notices

This project vendors the following libraries as git submodules under `third_party/`. Each keeps
its own license file in its submodule.

| Library | License | Source | Used for |
|---|---|---|---|
| MinHook | BSD-2-Clause | https://github.com/TsudaKageyu/minhook | API/vtable inline hooking |
| Dear ImGui | MIT | https://github.com/ocornut/imgui | in-game debug/config overlay |
| OpenXR SDK (loader) | Apache-2.0 | https://github.com/KhronosGroup/OpenXR-SDK | OpenXR runtime client |

Vendored copies (not submodules) under `third_party/`:

| Library | License | Source | Used for |
|---|---|---|---|
| OpenVR SDK 2.15.6 (headers + win32 `openvr_api.dll`) | BSD-3-Clause | https://github.com/ValveSoftware/openvr @ 0924064 | the SteamVR shim (`src/tools/ovrshim/`) talks to SteamVR through it; see `third_party/openvr_headers/PROVENANCE.txt` for SHA-256 pins |

Adapted code:

- **BioShock Trilogy VR Left-Hand Edition by Owloeb**
  (https://github.com/Owloeb/bioshock-trilogy-vr-lefthand, commit
  `7734c62306f386b38845ef8a35d6fefaf93065c5`, MIT) - independent off-hand
  tracking, controller haptics, recoil feedback, and plasmid calibration were
  used as implementation references. This fork adapts those features without
  the source branch's two-handed-grip system. Required MIT notice:

  ```text
  MIT License
  Copyright (c) 2026 bioshock-vr contributors

  Permission is hereby granted, free of charge, to any person obtaining a copy
  of this software and associated documentation files (the "Software"), to deal
  in the Software without restriction, including without limitation the rights
  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
  copies of the Software, and to permit persons to whom the Software is
  furnished to do so, subject to the following conditions:

  The above copyright notice and this permission notice shall be included in all
  copies or substantial portions of the Software.

  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
  SOFTWARE.
  ```

- **Bioshock-Remastered-VR by BioVRDev** (https://github.com/BioVRDev/Bioshock-Remastered-VR,
  no license file published) - the SteamVR shim in `src/tools/ovrshim/` is adapted from their
  `OpenXRShim/` module (OpenXR-on-OpenVR). Copied and adapted with the author's explicit
  permission, given 2026-08-13: the two projects collaborate and share features both ways, and
  the author granted a green light to copy anything from that repository (recorded in
  `docs/RESEARCH.md`, "BioVRDev/Bioshock-Remastered-VR analysis"). Adapted files carry an
  attribution comment.

Reference code (not vendored, not linked):

- **REFramework** (MIT, https://github.com/praydog/REFramework) - portions of the VR/D3D11
  integration may be adapted; adapted files carry an attribution comment.
- **bioshock-remastered-headtracking** (MIT, https://github.com/itsloopyo/bioshock-remastered-headtracking)
  - the `PlayerCalcView` FName-chain scan and camera hook technique are ported from this project.
- **UEVR** (all rights reserved, https://github.com/praydog/UEVR) - studied for concepts only.
  No code is or may be copied from it.
