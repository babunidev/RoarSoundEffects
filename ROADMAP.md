# Roar Sound Effects — finished project and compatibility notes

**Status:** Finished — legacy addon. No further development planned.  
**Creative:** Babuni  
**Repository:** `babunidev/RoarSoundEffects` (formerly `ROARSounds`)  
**Installed addon:** `ROAR`

## A completed experiment

Restoring the existing, race-specific `/roar` sounds in a client that no longer played them was the original creative goal. The addon was developed, packaged and documented. That work is now considered finished, without plans for additional features, compatibility ports or maintenance.

This document replaces the earlier active-looking roadmap. Ideas and unverified behaviors recorded elsewhere remain historical notes, **not an outstanding task list**. The separate RoarForever project is unaffected by this decision.

## Existing implementation

- `ROAR/ROAR.lua`, `ROAR/ROAR.toc` and the historical `ROAR.zip` package.
- Sixteen references to built-in sounds for eight races and two sex variants.
- Text-emote detection for the local character and other players whose unit identities can be resolved.
- Per-sender 0.3-second duplicate suppression.
- No current addon-message protocol, settings panel or sound files distributed with the addon.

## Compatible clients

The TOC declares `## Interface: 30300` for a WoW 3.3-era client. The historical addon is expected to work **only where the client supports its APIs and contains the referenced roar sound files**. This has not been newly tested, and no specific client version is guaranteed compatible.

The earlier review identified limitations such as English-only text matching, unsupported races, name collisions, possible sender-resolution gaps and unverified parity between the ZIP and source folder. These are qualifications of the finished build, **not a planned testing or repair backlog**.

## Closure — November 1, 2026

With the creative history and relationship to RoarForever documented, the creative chose to leave this project complete, as it stands. Only documentation was updated for the status change; executable files, packaging, audio assets and the license were not modified or tested.

## Related development history

Roar Sound Effects (originally ROARSounds) belongs to the **voice-restoration branch** of these expressive WoW experiments, not to the action-slot emote-trigger family. The April 2026 implementation listens for recognized text-emote activity and tries to replay the race/sex-specific client roar sound. It does **not** provide an emote registry, automatically perform an emote on ability use, or generate custom audio. This creative approach later informed Roar Forever, although direct code inheritance has not been verified. The [cross-project record](docs/EMOTE_FAMILY_HISTORY.md) puts both branches in context.
