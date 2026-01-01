# Currency Core Commands

[![Discord](https://img.shields.io/badge/Discord-Join%20for%20Help-7289da)](https://discord.gg/ngQXHUbnKg)

## Overview

The **Currency Core Commands** are the essential foundation for the entire currency system. These commands handle configuration, balance checking, daily rewards, currency transfers, and leaderboards.

## Core Commands

| Command | File | Purpose |
|---------|------|---------|
| **ConfigSetup** | `ConfigSetup.cs` | Initialize all global variables |
| **Balance Check** | `BalanceCommand.cs` | Check currency balance |
| **Daily Claim** | `DailyRedemption.cs` | Claim daily currency reward |
| **Give Currency** | `GiveCommand.cs` | Transfer currency to others |
| **Leaderboard** | `LeaderboardCommand.cs` | View top currency holders |

## Installation Order

**⚠️ IMPORTANT: Install in this exact order:**

### 1. ConfigSetup.cs (MUST BE FIRST)

This is the foundation for ALL currency commands.

```
Location: Currency/Core/Config-Setup/ConfigSetup.cs
Chat Command: None (run manually from StreamerBot)
Priority: ⚠️ CRITICAL - Run before anything else
```

**What it does:**
- Initializes ALL global variables
- Sets currency name and key
- Configures all game settings
- Sets up Discord logging
- Must be run BEFORE any other currency command

**How to run:**
1. Import ConfigSetup.cs into StreamerBot
2. Edit settings (currency name, Discord webhook, etc.)
3. Run the action manually
4. Verify you see success message in chat
5. Check Global Variables to confirm settings are saved

### 2. BalanceCommand.cs

```
Location: Currency/Core/Balance-Check/BalanceCommand.cs
Chat Command: !balance
Priority: Essential
```

**What it does:**
- Lets viewers check their current currency balance
- Returns balance as a chat message
- Logs balance checks to Discord

### 3. DailyRedemption.cs

```
Location: Currency/Core/Daily-Claim/DailyRedemption.cs
Chat Command: !daily
Priority: Highly Recommended
```

**What it does:**
- Gives users a daily currency reward
- 24-hour cooldown
- Tracks streak bonuses
- Prevents same-day claims

### 4. GiveCommand.cs (Optional)

```
Location: Currency/Core/Give-Coins/GiveCommand.cs
Chat Command: !give @user amount
Priority: Optional
Permission: Moderator/Broadcaster recommended
```

**What it does:**
- Transfer currency from one user to another
- Moderator command (for giveaways, rewards)
- Validates sender has enough currency
- Prevents negative amounts

### 5. LeaderboardCommand.cs (Optional)

```
Location: Currency/Core/Leaderboard/LeaderboardCommand.cs
Chat Command: !leaderboard
Priority: Optional
```

**What it does:**
- Displays top 5 currency holders
- Shows current balances
- Creates competition among viewers

## Quick Start Guide

### Step 1: Configure Your Currency

1. Open `ConfigSetup.cs`
2. Find the currency configuration section (lines 24-25):
   ```csharp
   CPH.SetGlobalVar("config_currency_name", "Cub Coins", true);
   CPH.SetGlobalVar("config_currency_key", "cubcoins", true);
   ```
3. Change "Cub Coins" to your preferred currency name
4. Save the file

### Step 2: Configure Discord Logging (Optional)

1. Still in `ConfigSetup.cs`, find line 356:
   ```csharp
   string discordWebhookUrl = "YOUR_WEBHOOK_URL_HERE";
   ```
2. Create a Discord webhook in your server
3. Paste the webhook URL
4. Save the file

### Step 3: Run ConfigSetup.cs

1. In StreamerBot, go to Actions tab
2. Find the ConfigSetup action
3. Click **Run** (or test button)
4. You should see a success message in chat
5. **Verify**: Go to Settings → Global Variables to confirm all variables are set

### Step 4: Install Core Commands

Import each command file:
1. Go to Actions → Import
2. Select the .cs file
3. Add chat command trigger
4. Test in chat

## Configuration

### Currency Settings

All settings are in `ConfigSetup.cs`:

```csharp
// CURRENCY CONFIGURATION
string currencyName = "Cub Coins";  // Display name
string currencyKey = "cubcoins";    // Storage key (lowercase, no spaces)
```

### Daily Reward Settings

```csharp
// DAILY CLAIM SETTINGS (lines 90-95)
int dailyBaseReward = 100;           // Base daily amount
int dailyStreakBonus = 25;           // Bonus per streak day
int dailyMaxStreak = 30;             // Max streak days
int dailyStreakDecayHours = 48;      // Hours before streak resets
```

### Leaderboard Settings

```csharp
// LEADERBOARD SETTINGS (lines 340-342)
int leaderboardTopCount = 5;         // How many users to show
int leaderboardCooldownSeconds = 60; // Cooldown between uses
```

## Command Usage

### !balance
```
User: !balance
Bot: Username has $250 Cub Coins.
```

### !daily
```
User: !daily
Bot: ✅ Daily claimed! You received $100 Cub Coins!
     Streak: 5 days (Bonus: $125) | Balance: $350
```

### !give @user amount
```
Moderator: !give @viewer 500
Bot: @Moderator gave @viewer $500 Cub Coins!
```

### !leaderboard
```
User: !leaderboard
Bot: 💰 Top 5 Leaderboard:
     1️⃣ User1: $5,000
     2️⃣ User2: $4,500
     3️⃣ User3: $3,200
     4️⃣ User4: $2,800
     5️⃣ User5: $2,400
```

## Dependencies

### ConfigSetup.cs Dependencies

ConfigSetup.cs requires:
- StreamerBot (no other files needed)
- Discord webhook URL (optional, for logging)

### All Other Commands Depend On

**ConfigSetup.cs must be run first!**

Each command reads from these global variables:
- `config_currency_name`
- `config_currency_key`
- `discordLogWebhook` (optional)
- `discordLoggingEnabled` (optional)

## Troubleshooting

### ConfigSetup Issues

**Issue: ConfigSetup doesn't run**
- Make sure you're running it from StreamerBot Actions tab
- Check for syntax errors in the file
- Verify you have latest StreamerBot version

**Issue: Global variables not saving**
- Make sure "persistent" parameter is `true`
- Check StreamerBot Settings → Global Variables
- Restart StreamerBot after running ConfigSetup

### Balance Command Issues

**Issue: Balance shows as $0 for everyone**
- Users start at $0 until they earn currency
- Run some earning commands (!work, !daily, etc.)
- Check Global Variables for correct currency key

**Issue: Balance not updating**
- Verify all commands use same currency key
- Check that ConfigSetup was run
- Look for errors in StreamerBot logs

### Daily Command Issues

**Issue: Can't claim daily even after 24 hours**
- Check system time is correct
- Verify cooldown settings in ConfigSetup.cs
- Clear user variables and try again

**Issue: Streak not incrementing**
- Streak only increments if claimed within decay period
- Default: Must claim within 48 hours
- Adjust `dailyStreakDecayHours` in ConfigSetup.cs

### Give Command Issues

**Issue: Can't give currency**
- Verify sender has enough currency
- Check that amount is positive
- Ensure target user exists

**Issue: Everyone can use give command**
- Add permission restriction to chat trigger
- Set to "Moderator" or "Broadcaster" only

### Leaderboard Issues

**Issue: Leaderboard shows no users**
- No users have earned currency yet
- Run some earning commands first
- Check currency key matches other commands

**Issue: Leaderboard shows wrong amounts**
- Verify currency key is consistent
- Check for multiple currency systems
- Clear and rebuild user variables

## Discord Logging

All core commands log to Discord if enabled:

### What Gets Logged

**Balance Checks:**
```
🎮 COMMAND
Command: !balance
User: Username
Details: Balance: $250
```

**Daily Claims:**
```
✅ SUCCESS
Daily Claimed
User: Username
Amount: $100
Streak: 5 days
New Balance: $350
```

**Currency Transfers:**
```
✅ SUCCESS
Currency Transfer
From: Moderator
To: Viewer
Amount: $500
```

**Errors:**
```
❌ ERROR
Command Error
Details: [Error message]
```

### Toggle Logging

```
!logging on     # Enable
!logging off    # Disable
!logging status # Check current state
```

## Best Practices

### Economy Balance

1. **Daily Rewards** - Set to 100-500 (baseline income)
2. **Streak Bonuses** - Reward consistent viewers
3. **Leaderboard** - Creates healthy competition
4. **Give Command** - Use for special events/giveaways

### Security

1. **Restrict Give** - Moderators/Broadcaster only
2. **Monitor Logs** - Watch for abuse
3. **Backup Variables** - Export Global Variables regularly
4. **Test First** - Test all commands before going live

### Viewer Engagement

1. **Announce Daily** - Remind viewers to claim !daily
2. **Leaderboard Resets** - Consider monthly/weekly resets
3. **Special Events** - Use !give for events/milestones
4. **Balance Integration** - Link to games and rewards

## Related Systems

### After Installing Core Commands

Next, install game commands from:
- `Currency/Games/` - 60+ earning and gambling games
- Each game has its own README with installation instructions

### Integration with Other Systems

Core commands work with:
- **All earning games** - Work, Battle, Fish, Hunt, etc.
- **All gambling games** - Slots, Coinflip, Dice, etc.
- **Special events** - Lottery, Trivia, Treasure Hunt

## Support

Need help with core currency commands?

- **Discord**: [https://discord.gg/ngQXHUbnKg](https://discord.gg/ngQXHUbnKg)
- **Individual Command READMEs**: Check each command folder
- **Main Currency README**: See parent folder

## File Locations

```
Currency/Core/
├── Config-Setup/
│   ├── ConfigSetup.cs
│   └── README.md
├── Balance-Check/
│   ├── BalanceCommand.cs
│   └── README.md
├── Daily-Claim/
│   ├── DailyRedemption.cs
│   └── README.md
├── Give-Coins/
│   ├── GiveCommand.cs
│   └── README.md
└── Leaderboard/
    ├── LeaderboardCommand.cs
    └── README.md
```

## Credits

**Created by**: HexEchoTV (CUB) | [GitHub](https://github.com/ThortonEllmers/Streamerbot-Commands)
**License**: Free for personal use only




