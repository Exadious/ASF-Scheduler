# BotScheduler

<p align="center">

![ASF Plugin](https://img.shields.io/badge/ArchiSteamFarm-Plugin-blue)
![Platform](https://img.shields.io/badge/Platform-.NET-green)
![License](https://img.shields.io/github/license/exadious/ASF-Scheduler)
![Release](https://img.shields.io/github/v/release/exadious/ASF-Scheduler)

</p>

BotScheduler is an **ArchiSteamFarm (ASF)** plugin that automatically starts and stops your bots according to configurable cron schedules.

Whether you only want your bots running during the day, overnight, or on specific weekdays, BotScheduler lets you automate everything with simple ASF commands.

---

## ✨ Features

* 📅 Schedule automatic bot startup and shutdown
* ⏰ Uses standard cron expressions
* 🤖 Supports one, multiple, or all bots
* 🔄 Enable or disable schedules at any time
* ▶️ Manually execute scheduled start/stop actions
* 💬 Fully controlled through ASF commands

---

# Installation

1. Download ASF-BotScheduler.zip from the latest release.
2. Navigate to the plugins directory of your ArchiSteamFarm installation.
3. Create a new folder (ArchiSteamFarm.CustomPlugins.BotScheduler) inside the plugins directory.
4. Extract the contents of the downloaded .zip file into the folder you just created.

Your directory structure should look similar to this:

```text
ArchiSteamFarm/
├── config/
├── plugins/
│   └── ArchiSteamFarm.CustomPlugins.BotScheduler/
│       ├── ArchiSteamFarm.CustomPlugins.BotScheduler.dll
│       └── ...
├── logs/
└── ArchiSteamFarm.exe
```

3. Restart ArchiSteamFarm.
4. Check the ASF log to verify that the plugin has been loaded successfully.

---

# Commands

| Command                                         | Description                   |
| ----------------------------------------------- | ----------------------------- |
| `!scheduler list`                               | List all configured schedules |
| `!scheduler <name> new "<start>" "<stop>" @ALL` | Create a new schedule         |
| `!scheduler <name> show`                        | Show schedule details         |
| `!scheduler <name> edit start "<cron>"`         | Change start cron             |
| `!scheduler <name> edit stop "<cron>"`          | Change stop cron              |
| `!scheduler <name> edit bots Bot1,Bot2`         | Assign bots                   |
| `!scheduler <name> enable`                      | Enable schedule               |
| `!scheduler <name> disable`                     | Disable schedule              |
| `!scheduler <name> runstart`                    | Execute start immediately     |
| `!scheduler <name> runstop`                     | Execute stop immediately      |
| `!scheduler <name> delete`                      | Delete schedule               |

---

# Examples

### Start all bots every weekday at 08:00 and stop them at 22:00

```text
!scheduler Workdays new "0 8 * * 1-5" "0 22 * * 1-5" @ALL
```

### Start at 07:30 instead

```text
!scheduler Workdays edit start "30 7 * * 1-5"
```

### Stop at 23:00

```text
!scheduler Workdays edit stop "0 23 * * 1-5"
```

### Use only specific bots

```text
!scheduler Workdays edit bots MainBot,AltBot
```

### Disable the schedule

```text
!scheduler Workdays disable
```

### Enable it again

```text
!scheduler Workdays enable
```

### Execute immediately

```text
!scheduler Workdays runstart
!scheduler Workdays runstop
```

---

# Cron Expressions

BotScheduler uses the standard **cron** format:

```text
┌──────── minute (0-59)
│ ┌────── hour (0-23)
│ │ ┌──── day of month (1-31)
│ │ │ ┌── month (1-12)
│ │ │ │ ┌─ day of week (0-7)
│ │ │ │ │
* * * * *
```

Example:

```text
0 8 * * 1-5
```

Meaning:

* Minute: **0**
* Hour: **08**
* Every day of the month
* Every month
* Monday through Friday

Useful examples:

| Expression     | Meaning            |
| -------------- | ------------------ |
| `0 8 * * *`    | Every day at 08:00 |
| `0 22 * * *`   | Every day at 22:00 |
| `0 */2 * * *`  | Every 2 hours      |
| `*/15 * * * *` | Every 15 minutes   |
| `0 8 * * 1-5`  | Weekdays at 08:00  |
| `0 10 * * 6,0` | Weekends at 10:00  |

---

# Notes

* Schedule names are case-insensitive.
* A schedule can control one or many bots.
* Use `@ALL` to target every configured ASF bot.
* Cron expressions are evaluated using the server's local time.

---

# Disclaimer

> This plugin is provided on **AS-IS** basis, without any guarantee at all. Author is not responsible for any harm, direct or indirect, that may be caused by using this plugin. You use this plugin at your own risk.
