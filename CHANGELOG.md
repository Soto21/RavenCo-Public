# Changelog

All notable changes from the base **TrinityConquer** to **RavenCo2**.

---

## [RavenCo2] — Custom Server Build

### ⚔️ Combat

- **Anti-macro protection** — 120ms debounce on basic melee attacks; same player cannot register two hits against the same target within that window
- **Weapon proc cooldowns** — Shield effect locked to 10s cooldown, Stigma effect to 20s; previously activated on every hit with no limit
- **Damage over time cap** — Monster poison capped at 1.5% max HP per second; instant kills from DoT are no longer possible
- **Unified damage system** — Physical, magic and ranged all processed through a single `DamageSystem.Apply()` / `ApplyMonster()` pipeline
- **Lucky Time consistency** — Lucky Time is resolved once per skill cast, not per target; all targets in a sector receive the same result
- **SpellScaleResolver** — Magic skill scaling by type and context (PvP / PvE) handled in a dedicated module
- **Sector / ScatterFire** — ScatterFire now supports up to 60 targets (up from 30)
- **Skill visual effects** — Phoenix, Celestial, Seizer, Earthquake and Boom now trigger proper particle effects
- **Stamina consumption** — Stamina is correctly consumed by skills that require it via a dedicated `UseStamina` call
- **DefensiveStance fix** — Flag was being removed twice; now works correctly as a toggle
- **PvP protection in AutoHunt** — Players in AutoHunt mode cannot be attacked by other players

---

### 📈 Progression

- **Epiphany system** — On rebirth at level 130 the player is automatically set back to their pre-rebirth level, retaining accumulated EXP; matches official Conquer Online behaviour
- **Rebirth attribute points** — Extra attribute points on rebirth calculated correctly per class and level; Water Tao can rebirth from level 110 with its own point table
- **RebirthStage3** — New rebirth stage with rounds and bosses to defeat tracked via bitmask per round
- **Team EXP formula** — Now multiplies by `TeamShareExpRate × UserExpRate × 4` with a per-member level factor relative to the mob; couples receive a ×2 bonus
- **Custom skill cooldowns** — Each skill can have an independent `CustomCoolDown` in ms; player receives a message showing remaining cooldown on blocked use
- **Socket Lucky Time proc** — Socket attempts during Lucky Time have their own proc chance

---

### 🎲 Drops & Rewards

- **DropRule system** — Custom drop rules per monster and map; items can fall to the ground or go directly to the player's inventory, with stack limits, level/BP/map filters and custom messages on direct delivery
- **Drop quality scaling** — Refined, Unique, Elite and Super quality rates now scale with monster level
- **Sea Potion drops** — Added specific sea potion IDs to monster drop generation
- **Earring / boot / shield generation** — These item types are now generated dynamically from ID ranges stored in the database rather than hardcoded values
- **VIP new player bonus** — First connection from a new IP address automatically grants VIP level 6 for 30 days; IP is cached so the reward only triggers once per connection origin

---

### 🤖 AutoHunt & Bots

- **Class-aware AutoHunting** — Dedicated hunters for Archer, Trojan, Fire Tao, Water Tao and a generic fallback; Water Tao with Backsword equipped automatically switches to magic attack mode
- **VIP AutoHunt loot config** — Per-player JSON config for exactly what to loot: Dragon Balls, Meteors, Plus Stones, money, gems, Tier 1 gems, +1 items, socketed items, Super 2-socket −5 items, quality items, blessed items, quality+blessed, auto-merge and split stacks of 5; setting persists between sessions
- **VIP gold summary** — Every 5 minutes displays gold looted in that window: `[VipHunting] In the last 5 minutes you looted X gold`
- **Follow system** — Players can follow another player automatically across the map; intelligent movement reaction, configurable minimum distance and max jump distance to avoid falling behind
- **Slave bot tiers** — T1 Elite (plus 12, unlimited sockets, SuperDragonGem), T2 Advanced (plus 8, max 6 slots, 2 sockets), T3 Basic (plus 6, max 3 slots); gear scales by bot level when no tier is assigned
- **Bot registry** — All slave bots registered in a global dictionary and findable by UID; bots appear with the owner's name: `[PlayerName's Slave]`; spawned asynchronously in batches with delays
- **PKBot rewrite** — Full rewrite with dedicated behaviour (`PkBotBehavior`), spawner (`PkBotSpawner`) and network layer (`BotNetworkClient`, `BotNetworkManager`); PKBots can now coordinate with each other
- **PKBot lucky drop** — On killing a PKBot, 90% chance the bounty is paid automatically (CPs go to killer); 10% chance the item drops as a free instant claim with a "Lucky drop!" message
- **PK Bot invasion** — Random world event where PKBots invade the map
- **Vendor Bot** — Automated shop bot; keep your stall open without being at the keyboard

---

### 👹 Monsters & Bosses

- **Monster attack modes** — Monsters now have configurable modes: Passive, Defensive, Aggressive, Guardian and Scripted (custom AI)
- **Monster family stats** — New per-family stats: `ExtraDamage`, `DamageReceptivity`, `PhysicalDefenseRate`, `MagicDefenseRate`, `MagicAttackRate`
- **King/Messenger scaling** — Mobs of type King or Messenger receive a ×15 defence multiplier; exclusion list configurable (e.g. BirdKing does not scale)
- **MonsterDeathHandler** — Centralised handler for drops and events triggered on boss death
- **CombatStats** — More precise damage and stat system for all mobs
- **Evil Abyss (map 1700)** — New exclusive zone with 7 unique bosses at fixed spawn positions; chain system: Satan (3644) → BeastSatan (3645) → FurySatan (3646) spawn in sequence on each kill; additional bosses: Hill Spirit, Swift Devil, Banshee, Cleansing Devil
- **Boss name fallback** — Bosses always display their correct name; "Boss 3644" can never appear
- **Intelligent respawn** — Server verifies the target cell is free before respawning a monster

---

### 🗺️ Map & Vision

- **RoleView rewrite — 19 bug fixes** (FIX-A through FIX-S):
  - Eliminated double entity spawns
  - Correct player ↔ player visibility reciprocity
  - Race conditions in Follow and Bot resolved
  - Items and mobs now use their own remove packets
  - Removed per-tick unnecessary allocations
  - Unified vision into a single loop for better performance
- **Block-range search** — Object lookup by blocks uses dynamic range based on vision threshold
- **Race condition fix** — Moving between blocks within the same tile no longer causes duplication
- **TryGetObject** — New method to find any entity by UID and type across the map

---

### 🛡️ Guild War

- **Door fix** — Doors reaching 0 HP now visually open with a mesh-change animation and a global server announcement
- **Score persistence** — Score is no longer cleared between rounds; only resets at the end of the full war
- **Initial score fix** — Bug that blocked guilds in the first war resolved

---

### 📋 Quests

- **Thread-safe quest dictionaries** — Migrated to `ConcurrentDictionary`; eliminates race conditions between threads
- **CheckQuest fix** — No longer returns true on empty source due to concurrent reads
- **Duplicate reward fix** — Finished quests cannot grant rewards a second time
- **Daily reset on login** — Specific quests reset automatically when the player logs in on a new day

---

### 🎰 Lottery

- **Auto-correction of invalid colours** — Invalid colour entries are fixed on file load; only chest armours may have black colour, all others are corrected to orange and written back to the file

---

### 💾 Stability & Performance

- **Parallel socket processing** — Packet processing moved from sequential to parallel; polling interval reduced from 5ms to 1ms; parallelism capped at CPU cores − 1; atomic flag prevents double-processing the same socket
- **Atomic file writes** — Player files built entirely in memory with `StringBuilder` then written in a single operation; the original file is never touched until the write succeeds — no data loss on crash
- **Player snapshot throttle** — Minimum 5 minutes between snapshots per player; up to 10 backups per player per category (items, spells, profs, quests, houses)
- **Serilog with daily rotation** — Server logs written to file with a 10,000-entry async buffer; no log loss under high load
- **MapManager async AI** — Monster AI runs in an independent async task per map; guard prevents overlapping ticks if the previous one hasn't finished
- **MaxOnline tracker** — Server tracks peak simultaneous player count since last start

---

### ✨ Quality of Life

- **Away message** — Players in away mode trigger an automatic PopUp and chat message to anyone who messages them: `"I'm away at the moment, please contact me later"`
- **Associates system** — Relationship types: Friends, Enemies, Partner, Mentor, Apprentice, PK Explorer; tracks kills, BP, current map and relationship duration per associate
- **Server launcher app** — Visual desktop app with tabs for API, AccountServer, GameServer and ConquerSite; real-time logs and start/stop buttons from a single interface
- **NpcHandler split** — Divided into Part1 and Part2 to support more simultaneous dialogues and NPCs
- **Item name normalisation** — NinjaKatana → NinjaWeapon, Earrings → Earring, Bow → ArcherBow, Backsword → TaoistBackSword
- **Equipment packet expansion** — `MsgShowEquipment` now includes SteedMount, RidingCrop, Tower and Fan
- **Durability normalisation** — Durability is sent to the client normalised to multiples of 10
- **Shield rebirth unlock** — Reborn players can equip any shield below level 70 regardless of class
- **Fan & Tower upgrades** — Fan and Tower items can now be upgraded without blocking

---

*Base: TrinityConquer — Custom build: RavenCo2 by Soto*
