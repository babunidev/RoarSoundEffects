# Roar Sound Effects — let Azeroth roar again

**By:** Babuni  
**GitHub repository:** `babunidev/RoarSoundEffects`  
**In-game addon folder / title:** `ROAR`  
**Declared interface:** `30300` (WoW 3.3-era, **not** the Vanilla 1.12 interface number)  
**Source of truth:** [`ROAR/ROAR.lua`](ROAR/ROAR.lua) and [`ROAR/ROAR.toc`](ROAR/ROAR.toc)  
**Verification:** Git/source inspection on 2026-10-26. In-game playback and client compatibility were not tested in this documentation pass.

**Project status: Finished — legacy addon.** The original implementation is complete and no further development is planned. The source and package remain available for players with a compatible World of Warcraft client. The manifest declares `Interface: 30300`, but successful playback and compatibility with any specific client build have not been verified in this documentation review. This is a development-lifecycle decision, not a compatibility guarantee.

This is my **Roar Sound Effects** project, formerly named **ROARSounds**. I wanted the `/roar` emote to have its audible character again, using the sounds already present in the game rather than distributing replacement audio. The GitHub repository is now [RoarSoundEffects](https://github.com/babunidev/RoarSoundEffects), while the installed addon retains the **ROAR** folder and source names.

ROARSounds restores a missing bit of character presence to the `/roar` emote by calling **existing World of Warcraft client sound files**. When the addon receives a recognized text-emote event, it can play the appropriate built-in roar for the player's own character or another identifiable character. The sound depends on the resolved character's race and sex.

There are **no bundled WAV replacements**. The addon maps 16 race/sex combinations to existing paths under `Sound\\Character\\PlayerRoars\\`; the game client must actually contain those files.

## How this began

A different World of Warcraft client had made the race-specific `/roar` sound one of my favorite small details. On a later client the emote had fallen silent, although its sound files still existed. Discovering that an addon could play those recordings again felt like restoring a missing piece of the game. Hearing my own character roar was especially rewarding.

The experience was something I wanted to share with family and guildmates. The source evolved from playing the local player's roar to detecting other players' text emotes and using identifiable units to find their sounds. It does not automatically enable playback for everyone in the group.

This experiment became a **creative predecessor of [RoarForever](https://github.com/babunidev/RoarForever)**. The connection is based on my recollection, recorded November 1, 2026; direct code inheritance has not been verified.

## What the addon can identify

The code recognizes the local player and attempts to resolve the text-emote sender using these unit contexts, in order:

1. Your own character.
2. Your current target.
3. Mouseover.
4. Focus.
5. Up to 40 raid unit references **if in a raid**, otherwise up to four party unit references **if in a party**.

If an emote sender cannot be resolved to one of those units, or there is no sound mapping, the source does **not** play a roar for them. Seeing a message in nearby emote chat does not by itself provide the race/sex information needed to choose a file. This is not a nearby-player scanning system and does not estimate distance.

The event is `CHAT_MSG_TEXT_EMOTE`, not a direct hook into the emote command. The recognizer searches English text for `" roars"` or `" roar"` (case-insensitive). That matching rule is broad, not language-independent, and should be tested for false positives and localized clients.

## Installation

The repository contains a ready-made folder `ROAR/` and a separate `ROAR.zip` download artifact.

To install from the **current repository files**, copy the `ROAR` folder so that these two files appear together:

```text
World of Warcraft/
└── Interface/
    └── AddOns/
        └── ROAR/
            ├── ROAR.toc
            └── ROAR.lua
```

Restart or reload the game, enable the addon where supported, and test the built-in `/roar` emote.

**Compatibility caution:** The TOC declares `## Interface: 30300` rather than `11200`. On a different era/build, the client may flag it as outdated or fail to support its event/API behavior. Do not change the interface number without testing the Lua code and sound paths on that client. The `ROAR.zip` archive exists in Git, but its contents were **not independently compared** with the working source during this review; inspect it before distributing it as the authoritative build.

## Supported sound mapping

The source maps both male and female variants of these eight race tokens: **Dwarf, Gnome, Human, NightElf, Orc, Tauren, Troll, and Undead**. `Scourge` returned by `UnitRace` is normalized to `Undead`.

There are no mappings for Blood Elf, Draenei or other races beyond those eight. For a race not in the table, the addon silently has no matching built-in path. The map is source-declared; successful playback of every asset has **not** been verified.

## Behavior and limitations

- Plays through `PlaySoundFile(path)` using game-supplied sound files.
- Initializes the local player's name/race/sex on `PLAYER_LOGIN`; refreshes the local mapping on a player `UNIT_MODEL_CHANGED` event.
- Suppresses candidate roar events from the **same normalized sender name** within **0.3 seconds** of one another.
- The timestamp is recorded *before* checking whether a nonlocal sender can be identified. An unresolved event may therefore consume that sender's brief cooldown without making a sound.
- The code strips realm suffixes from sender names; this may confuse different people sharing the same name across realms.
- Current source has **no slash commands, configuration panel, persistent saved variables, chat messages sent by the addon, or addon-to-addon communication**.
- It does not confirm physical distance beyond whether emote chat is delivered and whether a matching unit reference is available.

The sound remains a game-client asset. The addon creator authored this **detection and playback system**, not the underlying game audio.

## Project history

This repository began **April 19, 2026**, with a local-player-only emote sound restoration. It explored addon messaging for other players, then changed direction to **chat-event and unit-identity resolution** on April 22. A 0.3-second deduplication gate followed, along with packaging in the `ROAR/` folder and a ZIP upload.

That brief, traceable sequence is documented in the [development journal](docs/DEVLOG.md). The historic source changes are verified in commits; no missing personal discussions or feature approvals have been invented.

This is a **separate repository** from [`roar`](https://github.com/babunidev/BattleEmotesLegacy), [`roarr`](https://github.com/babunidev/BattleEmotes), [`ROARRunlimited`](https://github.com/babunidev/MultiActionEmotes), and [`RoarGuild`](https://github.com/babunidev/RoarGuildAddon). Those projects use similar names but different implementations.

## License and development documentation

The existing [MIT license](LICENSE) credits **Babuni (2026)**. The license covers repository software; it does not grant redistribution rights to Blizzard's game audio assets.

- [Creative concept](CONCEPT.md) · [Interaction and sound design](docs/DESIGN.md) · [Audio/content inventory](docs/CONTENT.md)
- [Technical architecture](docs/ARCHITECTURE.md) · [Decisions and unresolved questions](docs/DECISIONS.md) · [Narrative development journal](docs/DEVLOG.md)
- [Completion status and compatibility notes](ROADMAP.md) · [Changelog](CHANGELOG.md)
- [Human–AI collaboration](docs/AI_COLLABORATION.md) · [Developer/AI rules](AGENTS.md)

## Relationship to the action-emote projects

Roar Sound Effects (originally ROARSounds) belongs to the **voice-restoration branch** of these expressive WoW experiments, not to the action-slot emote-trigger family. The April 2026 implementation listens for recognized text-emote activity and tries to replay the race/sex-specific client roar sound. It does **not** provide an emote registry, automatically perform an emote on ability use, or generate custom audio. This creative approach later informed Roar Forever, although direct code inheritance has not been verified. [The wider project history](docs/EMOTE_FAMILY_HISTORY.md) separates action-triggered emote generators from sound playback and documents the Roar Guild and Flourish branches.
