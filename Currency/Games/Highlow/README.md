# Highlow Command

## Description
Guess if the next card will be higher or lower! Classic card guessing game with 2x payout on correct guesses.

## Command
`!highlow high/low [bet amount]`

## Features
- Draw 2 cards (1-13 values)
- Guess if second card is higher or lower
- Correct guess = configured multiplier payout
- Tie = lose bet
- Short command aliases (h/l)
- Configurable min/max bet limits
- Discord logging for all guesses

## Configuration
Set in `ConfigSetup.cs`:
- `config_highlow_min_bet` - Minimum bet amount (default: 10)
- `config_highlow_max_bet` - Maximum bet amount (default: 500)
- `config_highlow_win_mult` - Win multiplier (default: 2)
- `config_currency_name` - Currency name for messages
- `config_currency_key` - User variable key for balance

## Dependencies
- `ConfigSetup.cs` (must be run first)

## How It Works
1. User runs `!highlow high/low [bet]`
2. Command validates choice and bet amount
3. Accepts "high", "low", "h", or "l" as valid choices
4. Checks user balance
5. Bet is deducted from user balance
6. Draw two cards (1-13 each)
7. Check if guess is correct:
   - **High**: Win if card2 > card1
   - **Low**: Win if card2 < card1
   - **Tie** (card1 = card2): Lose bet
8. If won, award configured multiplier
9. Announce result with both card values
10. All games logged to Discord (if enabled)

## Example Output
**Win (High):**
```
🎴 5 → 9 | [Username] guessed high and WON $200 Cub Coins! Balance: $700
```

**Win (Low):**
```
🎴 10 → 3 | [Username] guessed low and WON $200 Cub Coins! Balance: $700
```

**Loss:**
```
🎴 7 → 4 | [Username] guessed high and LOST $100 Cub Coins. Balance: $400
```

**Tie (Loss):**
```
🎴 8 → 8 | [Username] guessed high and LOST $100 Cub Coins. Balance: $400
```

**Invalid Usage:**
```
[Username], choose high or low! Usage: !highlow high/low 10-500
```

## Installation
1. Create a new C# action in StreamerBot
2. Copy the contents of `HighlowCommand.cs`
3. Set the trigger to `!highlow` command
4. Ensure `ConfigSetup.cs` has been run first
5. Test with `!highlow high [amount]` or `!highlow low [amount]` in chat

## Tips
- Roughly 50/50 odds (ties go to house)
- Simple, easy to understand
- Quick gameplay, no cooldown
- Use "h" or "l" for faster typing

---
Created by HexEchoTV (CUB) | [GitHub](https://github.com/HexEchoTV/Streamerbot-Commands)
