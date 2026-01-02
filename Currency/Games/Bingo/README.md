# Bingo Command

## Description
A luck-based gambling game where users bet currency to play bingo and earn rewards based on how many lines they match (0-5 lines).

## Command
`!bingo [bet amount]`

## Features
- Bet-based bingo gameplay
- Random line matching (0-5 lines)
- Higher lines = higher multiplier rewards
- Full house (5 lines) provides special jackpot message
- Configurable min/max bet limits
- No cooldown - play as often as you have currency
- Discord logging for all bingo attempts and results

## Configuration
Set in `ConfigSetup.cs`:
- `config_bingo_min_bet` - Minimum bet amount (default: 10)
- `config_bingo_max_bet` - Maximum bet amount (default: 500)
- `config_bingo_win_mult` - Win multiplier (default: 2)
- `config_currency_name` - Currency name for messages
- `config_currency_key` - User variable key for balance

## Dependencies
- `ConfigSetup.cs` (must be run first)

## How It Works
1. User runs `!bingo [bet]` with amount between min and max
2. Command validates bet amount and checks user balance
3. Bet is deducted from user balance
4. System randomly generates 0-5 matching lines
5. Winnings calculated: `betAmount * (lines * 0.8)`
   - 0 lines = lose entire bet
   - 1 line = 0.8x (partial return)
   - 2 lines = 1.6x
   - 3 lines = 2.4x
   - 4 lines = 3.2x
   - 5 lines = 4.0x (FULL HOUSE!)
6. Winnings added to balance and result announced
7. All activity logged to Discord (if enabled)

## Example Output
**Full House (5 lines):**
```
🎉 BINGO! [Username] got 5 lines and won $400 coins! Balance: $1200
```

**Partial Win (3 lines):**
```
📋 3 lines! [Username] won $240 coins! Balance: $740
```

**Loss (0 lines):**
```
❌ No lines! [Username] lost $100 coins. Balance: $400
```

**Insufficient Funds:**
```
[Username], you need $100 coins!
```

**Invalid Usage:**
```
[Username], usage: !bingo 10-500
```

## Installation
1. Create a new C# action in StreamerBot
2. Copy the contents of `BingoCommand.cs`
3. Set the trigger to `!bingo` command
4. Ensure `ConfigSetup.cs` has been run first
5. Test with `!bingo [amount]` in chat

---
Created by HexEchoTV (CUB) | [GitHub](https://github.com/HexEchoTV/Streamerbot-Commands)
