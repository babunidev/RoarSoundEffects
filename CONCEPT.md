# Roar Sound Effects — concept and creative purpose

**By:** Babuni  
**Addon as installed:** ROAR  
**Document status:** Source-based reconstruction supplemented by Babuni's 2026-11-01 recollection; not an original brainstorming transcript.

## Giving a familiar emote its voice

For me, a character's roar should be something players can hear as well as read. I gave this original **ROARSounds** experiment the clearer portfolio name **Roar Sound Effects** while keeping its historical installed **ROAR** identity.

The project began with a small game-world observation: the player may see the text of a character's `/roar` emote without hearing the race-specific roar that helps the gesture feel alive. ROARSounds makes that expressive moment audible again by selecting a **built-in game sound** rather than inventing or replacing the sound palette.

The project's subject is presence and immersion, not statistics, combat advantage, UI ornament or voice chat. It is an auditory companion to a deliberate roleplay gesture. The sound should make a textual action feel more physical and characterful.

## Recovering a familiar voice

An earlier WoW client had made me love the sound of `/roar`. Finding the emote silent on another client—even while the sound files were still present—was the motivation for ROARSounds. The first reward was hearing my own character roar again; sharing that sound with family and guildmates became a larger ambition.

This recollection, supplied November 1, 2026, adds the human reason behind the source history. ROARSounds is a **creative predecessor** to [RoarForever](https://github.com/babunidev/RoarForever), but this does not establish that the later addon reuses its code. Other-player playback remains limited by what the client's unit APIs can identify.

## Expanding who can be heard

The earliest committed code responded to the local player's own roar. Later April commits attempted to let other addon users hear roaring over explicit addon communication. That approach was subsequently removed in favor of recognizing nearby `CHAT_MSG_TEXT_EMOTE` messages and identifying sender race/sex from an accessible game unit: target, mouseover, focus, group or raid roster.

This shift is a **documented implementation iteration**. It reduces protocol coordination but introduces limits: a text speaker must correspond to an identifiable unit, and the message text must match the addon's English substring rules. The exact original reasoning for abandoning addon messages was not recorded in the available Git messages; do not invent an approval conversation.

## A deliberately small footprint

The current code contains one Lua file and one TOC file. There are no config menus, custom sound downloads, character statistics, accounts, backend servers, emote macros or scheduled timers. A short, sender-specific gate prevents rapid duplicate playback. The user still chooses when to use `/roar`; this addon observes and reacts.

Eight races with male/female sound variants are declared; the addon uses client assets and cannot create audio for an unsupported race. Its TOC targets `30300`, so WoW versions other than that era need explicit compatibility tests.

## Related work, separate history

ROARSounds remains a distinct implementation from the action-slot-controlled `roar`, `roarr`, `ROARRunlimited`, `RoarGuild`, and later RoarForever. Its creative connection to RoarForever is established by Babuni's recollection; direct code lineage and release compatibility must be verified independently.

Babuni remains the original creative director. Technical and documentation assistance from AI must be attributed separately and only when supported by records.
