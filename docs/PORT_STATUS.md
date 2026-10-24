# Development status — Overburden for PS Vita

**Public status: in development, no release yet. Latest internal build: R9.**

These are development tests, not guarantees about a release build.

| Area | Status | Notes |
| --- | --- | --- |
| Boot | Working on physical Vita | 960×544 animated splash, CapUnlocker required |
| Main menu / pause | Working | Select toggles 4:3 / 16:9 with no on-screen label (R9) |
| Gameplay | Playable | Intro, bunker and final level reachable |
| 3D rendering | Experimental native GXM | Textured unlit meshes, CPU skinning, distance culling, triangle budget |
| Lighting / effects | Not implemented | No lights, shadow maps, fog or screen filters; CPU particles and contact shadows as substitutes |
| Audio | Working | Mixer on CPU3 through CapUnlocker |
| Loading | Slow | R9 removes most load-time logging and switches textures from WebP to PNG |
| Public downloadable build | Not available | No VPK, game files or game_data are published |

## Performance

Latest device logs (R8): about 45 FPS in the main menu and 28–35 FPS in gameplay. Physics costs 13–16 ms per 30 Hz step, the largest remaining part of the frame. 3D submission is bounded by an adaptive triangle budget.

R9 changes, pending device confirmation:

- Meshes are drawn whole or not at all, so objects are no longer cut in half at the budget limit.
- Walls and large room structure are never removed by the adaptive budget.
- The budget follows a moving average with small steps, and objects drawn in the previous frame keep priority, reducing flickering while the camera moves.
- Per-node load logging is limited to large scenes, and texture payloads use PNG instead of WebP lossless for cheaper decoding.
- The device log records the time between pressing Start and the level being ready.

## Known issues

- Long loading after pressing Start.
- Objects can still pop in and out in dense rooms because of the triangle budget.
- Unstable FPS, mainly from physics.
- The original color-limit/dither/vignette/grime filter and all dynamic lighting are missing.

## Public files policy

This repository contains documentation only. No VPK, compiled port, proprietary game files, imported game caches or patcher are provided.

## References

- [Overburden on itch.io](https://notsospecialgames.itch.io/overburden)
- [Godot 4 Vita](https://github.com/WolffsRoom/godot4-vita)
- [README](../README.md)
