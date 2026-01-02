# Dig Command

## Description
Grab your shovel and dig for treasures! Find various items with different rarity levels and rewards.

## Command
`!dig`

## Features
- 6 different discoverable items with varying rarity
- Treasure chest (2% chance) = 400 coins
- Ring (5% chance) = 200 coins
- Old coins (15% chance) = 100 coins
- Ancient pot (20% chance) = 60 coins
- Bones (25% chance) = 30 coins
- Worm (33% chance) = 5 coins
- Minutes-based cooldown
- Discord logging for all digs

## Configuration
Set in `ConfigSetup.cs`:
- `config_dig_cooldown_minutes` - Cooldown in minutes (default: 10)
- `config_currency_name` - Currency name for messages
- `config_currency_key` - User variable key for balance

**Note**: Dig rewards are hardcoded in the command, not in config.

## Dependencies
- `ConfigSetup.cs` (must be run first)

## How It Works
1. User runs `!dig` command
2. Command checks cooldown (minutes since last dig)
3. If on cooldown, displays time remaining (minutes + seconds)
4. Roll random chance for item rarity
5. Award corresponding reward based on item found
6. Add coins to user balance
7. Set cooldown timer
8. Announce discovery with item emoji and reward
9. All digs logged to Discord (if enabled)

## Discoverable Items
| Item | Emoji | Chance | Reward |
|------|-------|--------|--------|
| Treasure Chest | 💰 | 3% | 400 coins |
| Ring | 💍 | 5% | 200 coins |
| Old Coins | 🪙 | 15% | 100 coins |
| Ancient Pot | ⚱️ | 20% | 60 coins |
| Bones | 🦴 | 25% | 30 coins |
| Worm | 🪱 | 30% | 5 coins |

## Example Output
**Legendary Find:**
```
🪦 [Username] dug up 💰 TREASURE CHEST and earned $400 Cub Coins! Balance: $1200
```

**Common Find:**
```
🪦 [Username] dug up 🪱 WORM and earned $5 Cub Coins! Balance: $805
```

**Cooldown Active:**
```
[Username], your shovel is dirty! Wait 7m 32s.
```

## Installation
1. Create a new C# action in StreamerBot
2. Copy the contents of `DigCommand.cs`
3. Set the trigger to `!dig` command
4. Ensure `ConfigSetup.cs` has been run first
5. Test with `!dig` in chat

## Tips
- Short cooldown encourages frequent use
- Guaranteed rewards (no risk of losing coins)
- Rarity system creates excitement for rare finds
- Great for viewers who want guaranteed income

---
Created by HexEchoTV (CUB) | [GitHub](https://github.com/HexEchoTV/Streamerbot-Commands)
