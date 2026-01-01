# Balance Check Command

[![Discord](https://img.shields.io/badge/Discord-Join%20for%20Help-7289da)](https://discord.gg/ngQXHUbnKg)

## Overview

The **Balance Check Command** allows viewers to check their current currency balance in your Twitch chat. When a viewer types `!balance`, the bot will respond with how much currency they currently have.

## What This Command Does

- Responds to `!balance` command in Twitch chat
- Displays the user's current currency balance
- Works with the customizable currency system (default: "Cub Coins")
- Logs all balance checks to Discord (if logging is enabled)
- Automatically initializes user balance to 0 if they've never earned currency before

## Dependencies

This command requires the following files to be set up first:

1. **ConfigSetup.cs** (Required)
   - Location: `Currency/Core/Config-Setup/ConfigSetup.cs`
   - Purpose: Initializes currency name and key global variables
   - **Must be run before using this command**

2. **Discord Logging** (Optional)
   - Built-in to this command file
   - Purpose: Logs balance checks to Discord webhook
   - Only works if Discord webhook is configured in ConfigSetup.cs

## Installation

### Step 1: Run ConfigSetup.cs First

Before installing this command, you **must** run `ConfigSetup.cs`:

1. Open StreamerBot
2. Go to **Actions** tab
3. Import `Currency/Core/Config-Setup/ConfigSetup.cs`
4. Edit the file to configure your currency settings (lines 24-25):
   ```csharp
   CPH.SetGlobalVar("config_currency_name", "Cub Coins", true);
   CPH.SetGlobalVar("config_currency_key", "cubcoins", true);
   ```
5. **Run the action** to initialize all global variables
6. You should see a success message in chat

### Step 2: Import Balance Command

1. In StreamerBot, go to **Actions** tab
2. Click **Import** (bottom left)
3. Select `Currency/Core/Balance-Check/BalanceCommand.cs`
4. Click **Import**

### Step 3: Create Chat Command Trigger

1. In the action you just imported, go to **Triggers** tab
2. Click **Add** → **Chat Message** → **Command**
3. Configure the trigger:
   - **Command**: `!balance`
   - **Permission**: Everyone
   - **Enabled**: Check this box
4. Click **OK**

### Step 4: Test the Command

1. Go to your Twitch chat
2. Type: `!balance`
3. The bot should respond with your current balance (likely $0 if you haven't earned any currency yet)

## Usage

### Basic Command

```
!balance
```

**Response:**
```
[Username] has $0 Cub Coins.
```

### After Earning Currency

Once you've earned currency through games or daily claims:

```
!balance
```

**Response:**
```
[Username] has $250 Cub Coins.
```

### Who Can Use This Command?

By default, **anyone** in your chat can use `!balance`. You can restrict it by:

1. Going to the action's **Triggers** tab
2. Editing the Chat Command trigger
3. Changing **Permission** to:
   - Moderators only
   - Subscribers only
   - VIPs only
   - Custom permission

## Configuration

### Changing Currency Name

To change what your currency is called:

1. Open `ConfigSetup.cs`
2. Find line 24:
   ```csharp
   CPH.SetGlobalVar("config_currency_name", "Cub Coins", true);
   ```
3. Change "Cub Coins" to your preferred name (e.g., "Points", "Gold", "Coins")
4. **Run ConfigSetup.cs again** to save changes

### Changing Currency Storage Key

The currency key is the internal variable name used to store balances:

1. Open `ConfigSetup.cs`
2. Find line 25:
   ```csharp
   CPH.SetGlobalVar("config_currency_key", "cubcoins", true);
   ```
3. Change "cubcoins" to your preferred key (lowercase, no spaces)
4. **Important**: Only change this if you're setting up for the first time
5. **Run ConfigSetup.cs again** to save changes

### Customizing the Response Message

To change how the bot responds:

1. Open `BalanceCommand.cs`
2. Find line 30:
   ```csharp
   CPH.SendMessage($"{userName} has ${balance} {currencyName}.");
   ```
3. Customize the message format:
   ```csharp
   // Examples:
   CPH.SendMessage($"💰 {userName}, you have ${balance} {currencyName}!");
   CPH.SendMessage($"{userName}'s balance: ${balance} {currencyName}");
   CPH.SendMessage($"@{userName} → ${balance} {currencyName}");
   ```

## What Gets Logged?

If Discord logging is enabled, the following is logged when someone checks their balance:

### Command Execution Log (Purple)
```
🎮 COMMAND
Command: !balance
User: [Username]
Details: Balance: $250
```

### Error Log (Red)
Only appears if something goes wrong:
```
❌ ERROR
Balance Command Error
Error: [Error message]
```

## Troubleshooting

### Issue: Bot doesn't respond to !balance

**Solutions:**
1. Make sure you've run **ConfigSetup.cs** first
2. Check that the Chat Command trigger is **enabled**
3. Verify the command is set to `!balance` (case-insensitive)
4. Check StreamerBot logs for errors
5. Ensure StreamerBot is connected to Twitch

### Issue: Balance shows as $0 even though I earned currency

**Solutions:**
1. Verify you're using the correct currency key across all commands
2. Check Global Variables in StreamerBot to see if `config_currency_key` is set correctly
3. Make sure the game/earning commands are using the same currency system
4. Run `!balance` again - user variables initialize to 0 on first check

### Issue: Currency name shows as blank or "null"

**Solution:**
- You haven't run ConfigSetup.cs yet, or `config_currency_name` isn't set
- Open ConfigSetup.cs, set your currency name, and run it

### Issue: Command works but nothing logs to Discord

**Solutions:**
1. Discord logging might be disabled - Check ConfigSetup.cs line 360
2. Discord webhook might not be configured in ConfigSetup.cs (line 356)
3. Make sure `discordLoggingEnabled` is set to `true` in Global Variables
4. Verify your Discord webhook URL is valid

## Related Commands

- **!daily** - Claim daily currency reward
- **!give @username amount** - Transfer currency to another user
- **!leaderboard** - View top currency holders
- **All game commands** - Earn or gamble currency

## Technical Details

### How Balance is Stored

- User balances are stored as **Twitch User Variables**
- Variable key: Value from `config_currency_key` (default: "cubcoins")
- Data type: Integer (whole numbers only)
- Scope: Persistent per user across streams
- Default value: 0 (if user has never earned currency)

### Currency System Architecture

```
ConfigSetup.cs (Foundation)
     ↓
Global Variables Set:
  - config_currency_name
  - config_currency_key
     ↓
All Commands Read From Global Variables
     ↓
User Balances Stored as Twitch User Variables
```

## Support

Need help? Join our Discord for support:
- Discord: [https://discord.gg/ngQXHUbnKg](https://discord.gg/ngQXHUbnKg)
- Report issues on the GitHub repository

## File Information

- **File**: `BalanceCommand.cs`
- **Location**: `Currency/Core/Balance-Check/`
- **Created by**: HexEchoTV (CUB) | [GitHub](https://github.com/HexEchoTV/Streamerbot-Commands)
- **License**: Free for personal use only
- **Dependencies**: ConfigSetup.cs




