# GracePeriod

A lightweight PvP grace period plugin for Paper/Spigot servers. New players are protected from other players for a set amount of **online time**, and can end the protection early whenever they want.

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## Features

- **Automatic protection for new players:** anyone joining for the first time gets a grace period
- **Online time only:** the timer only counts down while the player is on the server
- **Two-way protection:** graced players can't hurt other players, and other players can't hurt them
- **Covers more than melee:** also blocks fire from other players and, optionally, splash and lingering potion effects
- **Players can end it early** with `/grace end`, with an optional confirmation step
- **Staff tools:** give, remove, inspect and reload from in-game or console
- **Persistent:** remaining time is saved to disk and survives restarts
- **Fully configurable messages** with `&` color codes

## Requirements

- Java 17+
- Paper, Spigot or a fork, Minecraft 1.13+

## Installation

1. Download `GracePeriod-1.0.0.jar` from the [Releases](../../releases) page.
2. Put it in your server's `plugins/` folder.
3. Restart the server.
4. Edit `plugins/GracePeriod/config.yml` if you want, then run `/grace reload`.

## Commands

| Command | Description | Permission |
|---|---|---|
| `/grace time` | Check your remaining grace time | `grace.use` |
| `/grace end` | End your grace period early (asks for confirmation if enabled) | `grace.use` |
| `/grace end confirm` | Confirm ending your grace period (within 30 seconds) | `grace.use` |
| `/grace time <player>` | Check another player's grace time | `grace.admin` |
| `/grace give <player> [minutes]` | Give a player a grace period (default duration if no minutes given) | `grace.admin` |
| `/grace remove <player>` | Remove a player's grace period | `grace.admin` |
| `/grace reload` | Reload the config | `grace.admin` |

## Permissions

| Permission | Default | Description |
|---|---|---|
| `grace.use` | everyone | Use `/grace time` and `/grace end` |
| `grace.admin` | op | Give, remove, inspect and reload grace periods |

## Configuration

`plugins/GracePeriod/config.yml`:

```yaml
# How long a NEW player's grace period lasts, in minutes of ONLINE time.
duration-minutes: 60

# Ask players to type "/grace end confirm" before their protection is removed.
confirm-end: true

# Also block splash/lingering potion effects between a graced player and other players.
block-potions: true

messages:
  prefix: "&7[&aGrace&7] &r"
  # ... all other messages are editable too
```

Placeholders available in messages: `{time}` and `{player}`.

## How it works

- A grace period is given automatically the first time a player joins (`hasPlayedBefore` is false).
- The remaining time counts down only while the player is online and is saved to `plugins/GracePeriod/data.properties`.
- While protected, damage between that player and other players is cancelled in both directions, including projectiles, fire and (optionally) potions.
- When the time runs out, the player is told and PvP is enabled for them.

## Building from source

```bash
git clone https://github.com/<your-username>/GracePeriod.git
cd GracePeriod
# build with your usual Maven/Gradle setup against the Spigot/Paper API
```

## License

Released under the [MIT License](LICENSE).
