# ⚔️ RavenCo — Custom Conquer Online Private Server

> A heavily modified Conquer Online private server built on top of TrinityConquer, rewritten and expanded with 50+ custom features across combat, progression, automation, world bosses and PvP events.

---

## 🌐 Connect

| | |
|---|---|
| 🖥️ Website | `Soto` |
| 💬 Discord | `Soto` |
| 📧 Contact | `YSoto` |

---

## ⚔️ Combat

- Balanced PvP & PvE damage — physical and magic calculated separately per context
- Critical hit caps — 65% in PvP, 50% in PvE
- Dodge & accuracy system with guaranteed hit floors
- Anti-macro protection — 120ms debounce on basic melee attacks
- Weapon proc cooldowns — Shield (10s), Stigma (20s)
- Monster DoT capped at 1.5% max HP/s — no instant kills from poison
- PvP protection while in AutoHunt mode

---

## 📈 Progression

- Custom EXP rates for character, skills and profession
- Team EXP bonus — couples receive ×2 multiplier
- Meteor upgrade system with balanced probabilities per level, quality and plus
- Socket system — double socket chance, Bless multiplier, Lucky Time procs
- **Epiphany system** — rebirth at 130 and jump straight back to your previous level
- Chi, Subclass and Mentor systems fully implemented
- RebirthStage3 with rounds and boss kill requirements

---

## 🎲 Drops & Rewards

- Drop system scaled by Battle Power across 7 tiers (150 → 350+)
- Automatic random events throughout the day: Double Drop, Double EXP, Dragon Ball Rain, Better Drops — always visible on screen
- Advanced DropRule system — custom drops per monster/map, direct-to-inventory items, stack limits, level/BP/map filters
- Lucky Time — double damage, damage reflection and special drops with independent rates
- Daily Lucky Time reset every midnight
- **VIP new player bonus** — first connection from a new IP gets VIP level 6 for 30 days automatically

---

## 🤖 AutoHunt & Bots

- **Class-aware AutoHunting** — dedicated logic for Archer, Trojan, Fire Tao, Water Tao and generic fallback; Water Tao with Backsword auto-switches to magic mode
- **VIP AutoHunt loot config** — configure exactly what to pick up per account (DBs, Meteors, gems, socketed items, blessed gear, quality items and more); saved in JSON per player
- **Follow system** — follow another player automatically across the map
- **Slave bots** — up to 20 per player with three tiers: T1 Elite, T2 Advanced, T3 Basic, each with scaled gear and stats
- **Vendor Bot** — leave your shop running without being at your keyboard
- VIP gold summary every 5 minutes showing total gold looted

---

## 👹 World Bosses

- 8 hourly world bosses: Snow Banshee, Terato Dragon, Thrilling Spook, Corn Devil, Ganoderma, Mummy Skeleton, Dark Spearman, Darkmoon Demon
- **Lava Beast** — rare spawn in FrozenGrotto6 announced globally
- **Evil Abyss (map 1700)** — exclusive zone with 7 unique bosses including a kill chain: Satan → Beast Satan → Fury Satan
- **PK Bot Invasion** — random world event where dangerous AI enemies invade; kill them for bounty and lucky drops

---

## 🏆 PvP Events & Tournaments

**Hourly tournaments**
Pass the Bomb · Dragon War · King of the Hill · Five N' Out · Frozen Sky · Last Man Standing

**Guild & Clan Wars**
- Guild War — every Sunday
- Elite Guild War — daily at 20:00
- Clan War — daily at 19:00, rotating through all cities
- Classic Clan War — daily at 14:00
- Pole Domination — 4 maps every hour in rotation, prizes in ConquerPoints

**Weekly scheduled events**
- Class PK War — Monday 18:00
- Capture the Flag — Wednesday 18:00
- Skill Team PK Tournament — Wednesday 19:55
- Elite PK Tournament — Friday 19:55
- Team PK Tournament — Saturday 18:55

**Mini-games**
Quiz Show · Treasure Thief · Knight Game · Top Fight · Couples PK War

---

## ✨ Quality of Life

- Away message — automatic reply sent to anyone who messages you while away
- Associates system — track friends, enemies, partners, mentors and PK explorers with BP, map and kill stats
- Server launcher — all server processes managed from a single visual desktop app with real-time logs
- Zero item loss on crash — player files written atomically; original file untouched until write succeeds
- Peak online players tracked since last server start

---

## 🛠️ Technical highlights

- Parallel socket processing — all players processed simultaneously, polling at 1ms
- Unified damage pipeline — physical, magic and ranged through a single system
- RoleView rewrite — 19 race conditions and vision bugs resolved
- Thread-safe quest system — ConcurrentDictionary throughout
- Serilog with daily log rotation and 10,000-entry async buffer
- MapManager async AI — monster AI runs independently per map with overlap protection
- Player snapshot throttle — max 10 backups per category, minimum 5 minutes between saves

---

## 📄 Changelog

See [CHANGELOG.md](./CHANGELOG.md) for a full breakdown of every change from the TrinityConquer base.

---

*Built with ❤️ by [Soto21](https://github.com/Soto21)*
