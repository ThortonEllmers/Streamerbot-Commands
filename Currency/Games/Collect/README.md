# Collect Command

## Description
Claim your periodic collection reward! A simple cooldown-based earning command with guaranteed payouts.

## Command
`!collect`

## Features
- Guaranteed rewards (no risk)
- Configurable reward range
- Hours/minutes cooldown tracking
- Simple, straightforward earning method
- Discord logging for all collections
- No bet or parameter required

## Configuration
Set in `ConfigSetup.cs`:
- `config_collect_min` - Minimum reward (default: 50)
- `config_collect_max` - Maximum reward (default: 150)
- `config_collect_cooldown_minutes` - Cooldown in minutes (default: 60)
- `config_currency_name` - Currency name for messages
- `config_currency_key` - User variable key for balance

## Dependencies
- `ConfigSetup.cs` (must be run first)

## How It Works
1. User runs `!collect` command
2. Command checks cooldown (minutes since last collection)
3. If on cooldown, displays time remaining (hours + minutes)
4. If available, calculates random reward between min and max
5. Adds reward to user balance
6. Sets cooldown for configured minutes
7. Announces collection with reward amount
8. All collections logged to Discord (if enabled)

## Example Output
**Success:**
```
📦 [Username] collected $104 Cub Coins! Balance: $704
```

**Cooldown Active:**
```
[Username], next collection in 0h 42m!
```

## Installation
1. Create a new C# action in StreamerBot
2. Copy the contents of `CollectCommand.cs`
3. Set the trigger to `!collect` command
4. Ensure `ConfigSetup.cs` has been run first
5. Test with `!collect` in chat

## Tips
- Collect is risk-free, making it great for new viewers
- Default 60-minute cooldown balances  rewards without spam
- Consider as an alternative to !daily for more frequent rewards
- Adjust cooldown based on your desired economy flow

---
Created by HexEchoTV (CUB) | [GitHub](https://github.com/HexEchoTV/Streamerbot-Commands)
