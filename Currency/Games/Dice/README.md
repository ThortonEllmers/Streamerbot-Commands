# Dice Command

## Description
Roll two dice and win based on your results! Doubles, lucky 7s, and high rolls earn different multiplier payouts.

## Command
`!dice [bet amount]`

## Features
- Roll 2 dice (1-6 each)
- Multiple win conditions with different payouts
- Double 6s = highest payout (10x default)
- Other doubles = 4x payout
- Lucky 7 = 3x payout
- High roll (10+) = 2x payout
- Configurable min/max bet limits
- Discord logging for all dice rolls

## Configuration
Set in `ConfigSetup.cs`:
- `config_dice_min_bet` - Minimum bet amount (default: 10)
- `config_dice_max_bet` - Maximum bet amount (default: 500)
- `config_dice_win_mult` - Base win multiplier (default: 2)
- `config_currency_name` - Currency name for messages
- `config_currency_key` - User variable key for balance

## Dependencies
- `ConfigSetup.cs` (must be run first)

## How It Works
1. User runs `!dice [bet]` with amount between min and max
2. Command validates bet amount and checks user balance
3. Bet is deducted from user balance
4. Roll two dice (each 1-6)
5. Calculate total and check for win conditions:
   - **Double 6s (total 12)**: Win mult × 5 (10x default)
   - **Other doubles**: Win mult × 2 (4x default)
   - **Lucky 7**: Win mult × 1.5 (3x default)
   - **Total 10-11**: Win mult × 1 (2x default)
   - **Total < 10**: Lose bet
6. If won, add winnings to balance
7. Announce result with dice values and outcome
8. All rolls logged to Discord (if enabled)

## Example Output
**Double 6s (Jackpot):**
```
🎲 [6] [6] = 12 | [Username] WON $1000 Cub Coins! Balance: $1500
```

**Other Doubles:**
```
🎲 [4] [4] = 8 | [Username] WON $400 Cub Coins! Balance: $900
```

**Lucky 7:**
```
🎲 [3] [4] = 7 | [Username] WON $300 Cub Coins! Balance: $800
```

**High Roll:**
```
🎲 [5] [6] = 11 | [Username] WON $200 Cub Coins! Balance: $700
```

**Loss:**
```
🎲 [2] [4] = 6 | [Username] LOST $100 Cub Coins. Balance: $400
```

## Installation
1. Create a new C# action in StreamerBot
2. Copy the contents of `DiceCommand.cs`
3. Set the trigger to `!dice` command
4. Ensure `ConfigSetup.cs` has been run first
5. Test with `!dice [amount]` in chat

## Winning Probabilities
- Double 6s: 2.78% (1/36)
- Other doubles: 13.89% (5/36)
- Lucky 7: 16.67% (6/36)
- High roll (10-11, no doubles): ~11.11%
- **Total win chance: ~44.45%**

---
Created by HexEchoTV (CUB) | [GitHub](https://github.com/HexEchoTV/Streamerbot-Commands)
