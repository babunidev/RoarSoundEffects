# Roar Sound Effects — creative and technical development journal

**Project creator and creative director:** Babuni  
**Retrospective authored:** 2026-10-26 from repository README, committed Lua/TOC and dated Git diffs. Original chat transcripts were not reconstructed or published.

## April 19, 2026 — letting the roar be heard

ROARSounds began with a narrow act of game-world restoration. The original `ROAR.lua` committed on **April 19, 2026** (`5d54503`) watched for an emote message from the player's own character. When text indicated a roar, it selected the corresponding built-in game audio using the character's race and sex. It did not create a new sound pack or require the user to configure an ability rotation; it simply made a familiar roleplay gesture audible.

This is the core creative idea associated with Babuni. It is expressed by the repository's purpose and first implementation. The initial commits do not preserve an inspiration conversation. Babuni's November 1, 2026 personal recollection, recorded below, now supplies the reason without inventing a transcript.

The earliest code listed race-specific sound variants in a nested table keyed by race and sex, including an alias for the Undead/Scourge naming. It subscribed to `PLAYER_LOGIN`, `UNIT_MODEL_CHANGED`, and `CHAT_MSG_TEXT_EMOTE` and used `PlaySoundFile`. At first it cared only about the speaker who installed the addon.

## April 20 — experimenting with communication

The first visible expansion (`0d1fafb`, **April 20**) flattened the race+sex map into combined identifiers and attempted to share roar IDs using addon messages. In that snapshot, a local roar could trigger `SendAddonMessage` toward a raid, party or guild, and other addon users could play the corresponding file after receiving `CHAT_MSG_ADDON`.

This matters because it documents an approach that did **not** remain in the finished version. It shows the authorial project exploring a larger experience: not just one's own roar, but sound from fellow players. It also introduced communication dependencies that a simple text-emote listener would not need.

On **April 22**, `ff9f8bf` developed the concept further with normalized names, unit-token lookup, and a range check for received addon messages. This stage tried to reconcile sender identity with the game-world position of the player rather than simply accepting every packet.

Git establishes the code path; it does not establish who suggested the addon-message strategy or how anyone assessed its success.

## April 22 — another direction, fewer moving parts

A subsequent April 22 change (`fcc2be8`) removed the outgoing/received addon-message protocol and moved toward resolving players from the text-emote event itself. The rewritten `FindUnitBySender` checks the player's own unit, then target, mouseover, focus, raid or party references. When it can identify a sender, `GetRoarIDForUnit` combines the race and sex into one of the mapping keys.

This change is the strongest technical **pivot** in the record. The desired experience—audible roars with a character-specific voice—stayed recognizable, but the implementation abandoned network coordination. It became reactive to chat messages the client was already receiving. The tradeoff is that somebody whose name appears in emote text may still be unknowable as a unit: the addon cannot pick their sound unless target/roster information is available.

A little later that same day, `42023c0` introduced a **0.3-second cooldown keyed by normalized sender name**. It is a pragmatic anti-duplication measure rather than a roleplay mechanic. The timing is recorded before the code verifies the sender's sound, so an unresolved event can briefly suppress a later one. The implementation is consistent with suppressing noise, but the original reasoning cannot be recovered from source alone.

## April 22 — making a distributable addon

The Lua and TOC were added inside a proper `ROAR/` directory (`2dde5e4`) and a `ROAR.zip` artifact uploaded (`8eac1fa`). The obsolete root-level files were then removed. The README subsequently told users to extract the ZIP or place the Lua and TOC inside an AddOns/ROAR folder.

This organizational move is easy to overlook but important for the future Babuni portfolio: a one-off script became something that another person could install, at least as intended by the committed package structure. The ZIP's bytes were not compared with the currently committed folder during this documentation review, so reproducibility remains unverified.

The packaged manifest declares **`Interface: 30300`**. This is an explicit 3.3-era interface version, unlike the `11200` manifests in some separate Vanilla projects. The source uses old event globals; that does not automatically prove its runtime works unchanged on any particular modern or legacy game distribution. Actual client installation and playback still need testing.

## September–October — a clean public account of what exists

On September 18, a wording change made the installation description provider-neutral. On October 26, earlier housekeeping updated author credit and supplied short project documents. The new documentation pass makes that history readable, with a practical README, an architecture description, an explicit race/sex sound inventory, a decisions register, and an actionable test plan.

The source now contains **16 declared WAV paths** across eight race families and two sex values. They are pointers to game-owned files, **not original recordings by Babuni**. It also has no custom slash-command UI, saved profile, addon communication or autonomous scanning system. Other-player playback is conditional on usable unit information.

**User contribution:** creative authorship and direction of the ROARSounds addon, reflected in the repo. **AI contribution in this session:** inspect source and Git history, interpret evidenced changes, write and commit Markdown documentation. **Not performed:** Lua/TOC/ZIP changes, audio extraction, live playback or sound-asset verification, or approval of additional behavior.

## The remaining creative questions

Should the addon try to recognize more races, offer player controls, or support clients beyond its declared TOC target? Is a silence-first response better than guessing when the speaker is not identifiable? Should matching be localized or made more precise? These are sensible **future questions for Babuni**, not decisions already made.

A publishable portfolio account should preserve both experiments—the temporary message protocol and the final chat-listener model—because the discarded solution shows how the work evolved, rather than pretending the current code was obvious from the beginning.

## November 1, 2026 — remembering the first roar

An earlier World of Warcraft client had made the distinctive `/roar` sound one of my favorite details. In another client the roar had become silent, even though the audio files were still there. Finding a way to call those existing sounds again felt like restoring something the game had lost. Hearing my own character roar mattered most, and sharing the experience with family and guildmates was part of the excitement.

The source records the progression from local playback through an addon-message experiment to a text-emote listener for identifiable players. My recollection supplies the motivation; the code supplies the technical limits. This was also the **creative predecessor of RoarForever**, though a direct code port has not been verified.

This is a later personal recollection, not a reconstructed conversation from April 2026. AI checked the implementation and integrated the account into the documentation; no addon code or in-game behavior was changed or tested.

## November 2026 — a clearer name for the sound experiment

The project that began as **ROARSounds** is now named **Roar Sound Effects** on GitHub. The idea was to let the sound of an in-game `/roar` match the character's race and sex, using the existing client sounds. I chose the more descriptive name while keeping the installed **ROAR** addon intact. My AI assistant revised the documentation at my request; it did not change Lua, game audio, packaging or verify playback during this pass.

## November 1, 2026 — a finished legacy addon

With the sound-restoration experiment documented, the project is finished. The original addon has served its intended purpose, and no further development of this version is planned. It can remain available to those using a client that supports the historical sounds and APIs, although current client compatibility was not retested.

My AI assistant recorded that decision in the project documentation. No Lua, TOC, ZIP, license or audio asset was changed.
