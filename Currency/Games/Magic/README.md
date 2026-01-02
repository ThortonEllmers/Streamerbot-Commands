# Magic Command

## Description
Cast magical spells for rewards! A themed earning command with mystical flair.

## Command
`!magic [bet amount]`

## Features
- Magic-themed gambling game
- Spell casting mechanics
- Configurable success rate and multipliers
- Win or lose based on magical power
- Configurable min/max bet limits
- Discord logging for all magic attempts
- Thematic messages for immersion

## Configuration
Set in `ConfigSetup.cs`:
- `config_magic_min_bet` - Minimum bet amount
- `config_magic_max_bet` - Maximum bet amount
- `config_magic_success_rate` - Success chance percentage
- `config_magic_win_mult` - Win multiplier
- `config_currency_name` - Currency name for messages
- `config_currency_key` - User variable key for balance

## Dependencies
- `ConfigSetup.cs` (must be run first)

## How It Works
1. User runs `!magic [bet]` with amount between min and max
2. Command validates bet amount and checks user balance
3. Bet is deducted from user balance
4. Cast spell with random success chance
5. If successful, win at configured multiplier
6. If failed, lose bet
7. Result announced with magical theme
8. All attempts logged to Discord (if enabled)

## Example Output
**Success:**
```
✨ [Username]'s spell succeeded and earned $[amount] coins! Balance: $[balance]
```

**Failure:**
```
🔮 [Username]'s spell failed and lost $[amount] coins! Balance: $[balance]
```

**Invalid Usage:**
```
[Username], usage: !magic [min]-[max]
```

## Installation
1. Create a new C# action in StreamerBot
2. Copy the contents of `MagicCommand.cs`
3. Set the trigger to `!magic` command
4. Ensure `ConfigSetup.cs` has been run first
5. Test with `!magic [amount]` in chat

## Tips
- Themed commands add variety to chat experience
- Adjust success rate for desired difficulty
- Great for fantasy or magic-themed streams

---
Created by HexEchoTV (CUB) | [GitHub](https://github.com/HexEchoTV/Streamerbot-Commands)
