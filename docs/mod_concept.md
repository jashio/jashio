# Vanilla+ Modernization Plan

A minimal-overhaul mod for **Star Wars: Empire at War** that keeps every vanilla faction, hero, and campaign beat intact while polishing visuals and usability. The focus is on higher-resolution assets, clearer readability, and modern quality-of-life changes that respect original balance and pacing.

## Vision and scope
- **Vanilla fidelity:** No new factions or lore deviations; reuse existing units, heroes, and tech trees.
- **Visual clarity:** Sharper textures, cleaned-up UI elements, and improved readability of battlefield effects.
- **Better camera:** Wider default zoom, smoother scroll speeds, and optional zoom presets exposed in `GameConstants.xml`.
- **More units, same roles:** Double land caps and roughly triple space caps so players can field fuller fleets and battalions without rewriting unit rosters.
- **QoL first:** Faster mod load, clearer tooltips, and small balance nudges that preserve original roles and counters.

## Core feature set
1. **Texture refresh (HD-friendly)**
   - Upscale and clean key ship, vehicle, and infantry textures using AI upscaling + manual touch-up; avoid changing silhouettes.
   - Replace low-res UI icons and cursors with crisp exports at 2x where possible.
   - Ensure mipmaps and alpha channels remain intact to avoid shimmering.

2. **Camera and controls**
   - Raise default max zoom distance for space and ground battles; expose min/max values in `GameConstants.xml` for user tweaks.
   - Smooth camera pan/zoom speeds and reduce edge-scroll acceleration to lower motion sickness.
   - Add a “cinematic zoom” hotkey preset that keeps tactical readability (e.g., caps at bomber torpedo visibility range).

3. **Readability and UI polish**
   - Standardize weapon VFX brightness and color to reduce visual noise, especially for turbolasers and missile trails.
   - Improve tooltip formatting: consistent color for damage types, clear armor class callouts, concise hero ability summaries.
   - Update loading screens and main menu backgrounds with cleaned-up vanilla art at higher resolution.

4. **Battle scale and unit caps**
   - Double the land battle cap to make combined-arms armies feel fuller without overwriting unit roles.
   - Expand space battle caps to 40–60 population depending on mode to support larger fleet compositions.
   - Keep reinforcement pacing readable: retain population costs per unit so composition choices remain meaningful.

5. **AI behavior for larger battles**
   - Allow tactical AI to spend the higher population budgets so it fields denser fleets and ground groups.
   - Encourage full carrier deployment so fighter/bomber complements show up in larger dogfights instead of being withheld.
   - Preserve vanilla tech timings; AI should prioritize filling caps rather than accelerating to super-units.

6. **Light-touch balance cleanup**
   - Keep vanilla counter triangles but normalize outlier units (e.g., underperforming corvettes vs. fighters, AT-ST vs. infantry).
   - Revisit population/pop-cap ratios so small fleets remain viable; avoid increasing overall battle scale.
   - Adjust build times and credit costs to reduce waiting without inflating income.

## Campaign and skirmish compatibility
- **Galactic Conquest:** Keep vanilla starting positions and story events; only adjust mission text and rewards if readability requires.
- **Skirmish:** Maintain current tech progression; focus on texture/UI upgrades and camera defaults that apply to all maps.
- **Multiplayer:** Avoid breaking sync—test camera constants and projectile effect changes in MP sessions before release.

## Production checklist
1. **Asset pass**
   - Export a target list of units/buildings per faction; batch-upscale textures, then hand-fix seams, decals, and emissive maps.
   - Regenerate `.alo` references if UV or texture dimensions change; verify hardpoint hookups remain intact.
   - Rebuild UI atlases at higher resolution and update XML references for icon sheets.

2. **Camera tuning**
   - Edit `Data/XML/GameConstants.xml` to raise `SPACE_CAMERA_MAX_HEIGHT` and ground equivalents; add comments for user edits.
   - Test zoom/pan values on large/small maps to ensure selection readability and projectile tracking remain clear.
   - Document optional user presets in `Text/MasterTextFile_*.txt` tooltips or a readme snippet.

3. **Battle scale & caps**
   - Use `GameConstants.xml` to set `Space_Population_Cap` and multiplayer equivalents to 60 (with optional 40 fallback if needed for stability) and land caps to 20.
   - Keep per-unit population costs intact; only adjust outliers where readability or pacing suffers.
   - Validate reinforcements and retreat timing at the higher caps to avoid spawn bottlenecks.

4. **AI tuning**
   - Ensure AI uses the expanded caps by raising `AI_Max_Space_Population_Cap`/`AI_Max_Land_Population_Cap` and enabling overbuild where safe.
   - Run AI-only skirmish matches to confirm full fleet deployment and carrier fighter launches.
   - Keep AI tech and build priorities otherwise unchanged to preserve vanilla pacing.

5. **Balance sanity pass**
   - Collect baseline DPS and survivability for key roles (interceptors, bombers, corvettes, frigates, heavies, artillery, hero units).
   - Nudge XML values only where vanilla outliers exist; keep hero abilities intact unless they obstruct readability.
   - Run quick skirmish AI matches to confirm no pop-cap or build-queue regressions.

6. **Packaging and performance**
   - Compress textures appropriately (DXT5/BC3 for alpha assets, DXT1/BC1 otherwise) and include mipmaps to minimize VRAM spikes.
   - Ship a minimal `GameConstants.xml` override plus updated art/UI; avoid bundling unused files to keep load times down.
   - Prepare a changelog highlighting camera defaults, texture upgrades, and any balance adjustments.

## Suggested folder structure (for the `Data/` directory)
```
Data/
  XML/
    GameConstants.xml      # camera values, population caps, and AI allowance for higher caps
    SpaceUnits/
    GroundUnits/
    Scripts/               # any QoL Lua hooks if needed
  Art/
    Models/
    Textures/              # upscaled textures with mipmaps
    UIFiles/               # updated icon atlases and loading screens
  Audio/
    SFX/
    Voices/
  Text/
    MasterTextFile_*.txt   # updated tooltips and changelog snippets
```

## Milestones
- **v0.1 Texture & Camera Preview:** Upscaled textures for core units, camera defaults raised, population caps increased, and documented user presets.
- **v0.3 Readability Pass:** UI/icon refresh, tooltip cleanup, standardized VFX brightness, AI tuned to use higher caps, and preliminary balance nudges.
- **v1.0 Vanilla+ Release:** Full texture set, stable camera/QoL defaults, MP-safe balance pass, large-fleet AI readiness, and packaged workshop build.

## Implementation kickoff
- Added `Data/XML/GameConstants.xml` with higher tactical population caps (space 60, land 20), raised camera ceilings, and AI population allowances so larger fleets are deployed.
- Next steps: validate stability of 60-cap space battles on large maps, then tune per-unit pop costs only if reinforcement pacing feels too slow.
