# Work Command

[![Discord](https://img.shields.io/badge/Discord-Join%20for%20Help-7289da)](https://discord.gg/ngQXHUbnKg)

## Overview

The **Work Command** allows viewers to earn currency by "working" various Twitch-related jobs. This is a fun, low-risk way to earn currency with a cooldown between uses.

## What This Command Does

- Randomly assigns a humorous Twitch-related job
- Earns random currency between configured min/max
- Enforces a cooldown period between work sessions (default: 30 minutes)
- Shows fun job descriptions (e.g., "worked as a Twitch mod", "lurked professionally")
- Logs all work attempts and earnings to Discord (if logging is enabled)
- No risk of losing currency

## Dependencies

This command requires the following files to be set up first:

1. **ConfigSetup.cs** (Required)
   - Location: `Currency/Core/Config-Setup/ConfigSetup.cs`
   - Purpose: Initializes work earnings and cooldown settings
   - **Must be run before using this command**

2. **Discord Logging** (Optional)
   - Built-in to this command file
   - Purpose: Logs all work attempts and earnings to Discord
   - Only works if Discord webhook is configured in ConfigSetup.cs

## Installation

### Step 1: Run ConfigSetup.cs First

1. Open StreamerBot
2. Go to **Actions** tab
3. Import `Currency/Core/Config-Setup/ConfigSetup.cs`
4. Edit the file to configure work settings (lines 40-42):
   ```csharp
   CPH.SetGlobalVar("config_work_min", 25, true);
   CPH.SetGlobalVar("config_work_max", 100, true);
   CPH.SetGlobalVar("config_work_cooldown_minutes", 30, true);
   ```
5. **Run the action** to initialize all global variables

### Step 2: Import Work Command

1. In StreamerBot, go to **Actions** tab
2. Click **Import** (bottom left)
3. Select `Currency/Games/Work/WorkCommand.cs`
4. Click **Import**

### Step 3: Create Chat Command Trigger

1. In the action you just imported, go to **Triggers** tab
2. Click **Add** → **Chat Message** → **Command**
3. Configure the trigger:
   - **Command**: `!work`
   - **Permission**: Everyone
   - **Enabled**: Check this box
4. Click **OK**

### Step 4: Test the Command

1. Type in chat: `!work`
2. You should earn currency and see a fun job message!
3. Try again immediately - you should get a cooldown message

## Usage

### Basic Command

```
!work
```

**Response:**
```
[Username] worked as a Twitch mod and earned $67 Cub Coins! Balance: $267
```

### Job Examples

The command randomly selects from these fun jobs:
- worked as a Twitch mod
- streamed for 8 hours
- farmed channel points
- clipped highlights
- raided another streamer
- donated subs
- posted emotes in chat
- lurked professionally
- organized raids
- became a VIP

### Cooldown Response

```
[Username], you're tired! Rest for 25m 30s before working again.
```

## Configuration

### Changing Minimum Earnings

To change the minimum amount earned:

1. Open `ConfigSetup.cs`
2. Find line 40:
   ```csharp
   CPH.SetGlobalVar("config_work_min", 25, true);
   ```
3. Change `25` to your preferred minimum
4. **Run ConfigSetup.cs again** to save changes

### Changing Maximum Earnings

To change the maximum amount earned:

1. Open `ConfigSetup.cs`
2. Find line 41:
   ```csharp
   CPH.SetGlobalVar("config_work_max", 100, true);
   ```
3. Change `100` to your preferred maximum
4. **Run ConfigSetup.cs again** to save changes

### Changing Cooldown Period

To change how often users can work:

1. Open `ConfigSetup.cs`
2. Find line 42:
   ```csharp
   CPH.SetGlobalVar("config_work_cooldown_minutes", 30, true);
   ```
3. Change `30` to your preferred minutes
4. **Run ConfigSetup.cs again** to save changes

**Examples:**
- `15` - Can work every 15 minutes
- `30` - Can work every 30 minutes (default)
- `60` - Can work every hour
- `120` - Can work every 2 hours

### Customizing Job Messages

To add your own custom jobs:

1. Open `WorkCommand.cs`
2. Find lines 71-82 (the jobs array)
3. Add or modify job descriptions:

```csharp
string[] jobs = {
    "worked as a Twitch mod",
    "streamed for 8 hours",
    "farmed channel points",
    "clipped highlights",
    "raided another streamer",
    "donated subs",
    "posted emotes in chat",
    "lurked professionally",
    "organized raids",
    "became a VIP",
    // Add your custom jobs here:
    "created epic memes",
    "danced on stream",
    "coded a bot",
    "hyped the chat"
};
```

### Customizing Success Message

To change the earnings message:

1. Open `WorkCommand.cs`
2. Find line 95:
   ```csharp
   CPH.SendMessage($"{userName} {jobDone} and earned ${earned} {currencyName}! Balance: ${balance}");
   ```
3. Customize the format:
   ```csharp
   // Examples:
   CPH.SendMessage($"💼 {userName} {jobDone}! Earned: ${earned} {currencyName} | Balance: ${balance}");
   CPH.SendMessage($"✅ Work complete! {userName} earned ${earned} for {jobDone}");
   ```

### Customizing Cooldown Message

To change the cooldown message:

1. Open `WorkCommand.cs`
2. Find line 60:
   ```csharp
   CPH.SendMessage($"{userName}, you're tired! Rest for {minutesLeft}m {secondsLeft}s before working again.");
   ```
3. Customize:
   ```csharp
   // Examples:
   CPH.SendMessage($"😴 {userName}, take a break! Work again in {minutesLeft}m {secondsLeft}s");
   CPH.SendMessage($"⏰ {userName}, cooldown: {minutesLeft}m {secondsLeft}s remaining");
   ```

## What Gets Logged?

If Discord logging is enabled:

### Command Execution Log (Purple)
```
🎮 COMMAND
Command: !work
User: [Username]
```

### Success Log (Green)
```
✅ SUCCESS
Work Reward Given
User: [Username]
Job: worked as a Twitch mod
Earned: $67 Cub Coins
Balance: $267
```

### Warning Log (Orange) - Cooldown
```
⚠️ WARNING
Work Cooldown Active
User: [Username]
Time remaining: 25m 30s
```

### Error Log (Red)
```
❌ ERROR
Work Command Error
User: [Username]
Error: [Error message]
```

## Troubleshooting

### Issue: Command doesn't respond

**Solutions:**
1. Make sure ConfigSetup.cs has been run
2. Check that the Chat Command trigger is **enabled**
3. Verify trigger is set to `!work` (case-insensitive)
4. Check StreamerBot logs for errors

### Issue: Cooldown seems wrong

**Solutions:**
1. Verify `config_work_cooldown_minutes` in Global Variables
2. Make sure you ran ConfigSetup.cs after changing the value
3. Cooldown is based on UTC time, not local time
4. Each user has their own independent cooldown

### Issue: Balance doesn't update

**Solutions:**
1. Check that `config_currency_key` is consistent
2. Use `!balance` to verify current balance
3. Check StreamerBot logs for errors
4. Verify ConfigSetup.cs was run properly

### Issue: Same job appears repeatedly

**Solution:**
- This is random - it's possible to get the same job multiple times
- The command uses C#'s Random class
- Over time, all jobs should appear roughly equally

## Advanced Features

### Adding Work Bonuses

To give bonuses for consecutive work sessions:

1. Open `WorkCommand.cs`
2. After line 68, add:
   ```csharp
   // Work streak bonus
   int workStreak = CPH.GetTwitchUserVarById<int>(userId, "work_streak", true);
   workStreak++;
   CPH.SetTwitchUserVarById(userId, "work_streak", workStreak, true);

   // Add 5% bonus per streak (max 50%)
   double bonusPercent = Math.Min(workStreak * 0.05, 0.50);
   earned = (int)(earned * (1 + bonusPercent));
   ```

### Adding Rare Job Outcomes

To add special rare jobs with higher rewards:

1. Open `WorkCommand.cs`
2. After line 84, add:
   ```csharp
   // 5% chance for epic job
   if (random.Next(1, 101) <= 5)
   {
       jobDone = "landed a sponsorship deal";
       earned *= 3; // Triple earnings!
   }
   ```

### Tracking Work Statistics

To track how many times a user has worked:

1. After line 89, add:
   ```csharp
   // Track total work count
   int workCount = CPH.GetTwitchUserVarById<int>(userId, "total_work_count", true);
   workCount++;
   CPH.SetTwitchUserVarById(userId, "total_work_count", workCount, true);
   ```

## Related Commands

Similar earning commands:
- **!fish** - Go fishing for currency
- **!hunt** - Hunt for currency
- **!mine** - Mine for currency
- **!forage** - Forage for currency
- **!scavenge** - Scavenge for currency
- **!dig** - Dig for currency
- **!beg** - Beg for currency (smaller amounts)
- **!daily** - Claim daily currency

## Economy Impact

### Earnings Per Hour

With default settings (25-100 coins, 30min cooldown):
- **Per use**: 25-100 coins (average: ~62 coins)
- **Per hour**: ~124 coins
- **Per day**: ~2,976 coins (24 hours active)

### Balancing Recommendations

**Conservative Economy:**
- Min: 15, Max: 50, Cooldown: 60 minutes

**Balanced Economy:**
- Min: 25, Max: 100, Cooldown: 30 minutes (default)

**Generous Economy:**
- Min: 50, Max: 200, Cooldown: 15 minutes

**Very Generous:**
- Min: 100, Max: 300, Cooldown: 10 minutes

## Support

Need help? Join our Discord for support:
- Discord: [https://discord.gg/ngQXHUbnKg](https://discord.gg/ngQXHUbnKg)
- Report issues on the GitHub repository

## File Information

- **File**: `WorkCommand.cs`
- **Location**: `Currency/Games/Work/`
- **Created by**: HexEchoTV (CUB) | [GitHub](https://github.com/HexEchoTV/Streamerbot-Commands)
- **License**: Free for personal use only
- **Dependencies**: ConfigSetup.cs




