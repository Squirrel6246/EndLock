<p align="center">
  <img src="main/icon.png" alt="lockend icon" width="128">
</p>

<h1 align="center">lockend</h1>

<p align="center">
  A lightweight, <b>server-side</b> Fabric mod that locks the End until you decide to open it.<br>
  Minecraft 26.2 &middot; Fabric &middot; Java 25
</p>

---

## What it does

lockend lets server owners lock the End dimension and its portals, then unlock it when they are ready, for example when a boss event or season launch begins. Players don't need to install anything, so vanilla clients can join.

## Features

- **Lock and unlock** the End with simple commands
- **Countdown unlocks** announced in chat, ending with an automatic unlock
- **Portal lock:** Eyes of Ender can't complete an End portal while locked
- **Partial fill control:** allow all frames except the last, or block placement entirely
- **Dimension lock:** optionally send anyone in or entering the End back to their spawn point
- **Private announcements:** show lock and unlock messages only to ops and chosen players
- **Clear feedback:** action-bar message, sound and particles when something is blocked
- **Ops bypass** for testing before launch
- **Persistent:** state survives restarts

## Installation

1. Install [Fabric Loader](https://fabricmc.net/) 0.19.3 or newer.
2. Install [Fabric API](https://modrinth.com/mod/fabric-api).
3. Put the lockend jar in your server's `mods` folder.
4. Start the server.

**Requirements:** Minecraft 26.2, Java 25, Fabric API. Not needed on the client.

## Commands

All commands need operator permission (level 2). The main command is `/lockend`, and `/endlock` works as an alias.

### Locking

| Command | Description |
|---|---|
| `/lockend lock [silent\|public]` | Lock the End |
| `/lockend unlock [seconds] [silent\|public]` | Unlock now, or after a countdown |
| `/lockend status` | Show the lock state and all settings |

### Behavior

| Command | Description |
|---|---|
| `/lockend partialfillallowed <true\|false>` | `true` (default): eyes can fill every frame except the last. `false`: no eyes can be placed while locked. |
| `/lockend lockdimension <true\|false>` | `true` (default): players are also kept out of the End. `false`: only portals are locked. |

### Visibility

| Command | Description |
|---|---|
| `/lockend announce <everyone\|ops>` | Default audience for lock, unlock and countdown messages |
| `/lockend notify add <player>` | Let a non-op player see private announcements (must be online) |
| `/lockend notify remove <name>` | Remove a player from the notify list |
| `/lockend notify list` | Show the notify list |

`silent` sends that one announcement (and its countdown) only to ops and the notify list. `public` forces it to everyone, which is useful if the default is set to `ops`.

### Examples

```
/lockend lock                      # lock the End
/lockend unlock 60                 # announce a 60 second countdown, then open it
/lockend unlock 30 silent          # same, but only ops and the notify list are told
/lockend announce ops              # make private announcements the default
/lockend notify add Steve          # Steve sees private announcements
```

## Configuration

State is saved to `config/lockend.json`. It is managed through the commands above, but you can edit it while the server is stopped.

```json
{
  "locked": false,
  "partialFillAllowed": true,
  "lockDimension": true,
  "publicAnnouncements": true,
  "notifyPlayers": {}
}
```

`notifyPlayers` maps player UUIDs to their last known names.

## FAQ

**Do players need the mod?** No. It is server-side only.

**Do ops get blocked?** No. Operators bypass all locks.

**What happens to players already in the End when it locks?** With `lockdimension` on, they are sent to their spawn point. With it off, they can stay.

**Does it work in singleplayer?** Yes, with cheats enabled so you can use the commands.

**Does it handle custom or unusual portal builds?** Last-frame detection is designed for standard 12-frame stronghold portals.

## Building from source

Requires JDK 25.

```
./gradlew build          # Linux / macOS
gradlew.bat build        # Windows
```

The jar is written to `build/libs/lockend-<version>.jar`.

## Credits

Inspired by the feature set of *Easy End Lock*. lockend is an independent, clean-room implementation and shares no code with it.

## License

MIT, as declared in `fabric.mod.json`.
