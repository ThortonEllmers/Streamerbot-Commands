# Keno Command

## Description
Play keno and match numbers for escalating rewards! Match 0-5 numbers with different multiplier payouts.

## Command
`!keno [bet amount]`

## Features
- Match 0-5 numbers
- Escalating multipliers based on matches
- 5 matches = 10x payout
- 4 matches = 5x payout
- 3 matches = 2.5x payout
- 2 matches = 1.5x payout
- 1 match = 0.5x (partial return)
- 0 matches = lose bet
- Configurable min/max bet limits
- Discord logging for all keno plays

## Configuration
Set in `ConfigSetup.cs`:
- `config_keno_min_bet` - Minimum bet amount (default: 10)
- `config_keno_max_bet` - Maximum bet amount (default: 500)
- `config_keno_max_mult` - Not used (legacy parameter)
- `config_currency_name` - Currency name for messages
- `config_currency_key` - User variable key for balance

## Dependencies
- `ConfigSetup.cs` (must be run first)

## How It Works
1. User runs `!keno [bet]` with amount between min and max
2. Command validates bet amount and checks user balance
3. Bet is deducted from user balance
4. System generates random number of matches (0-5)
5. Multiplier determined by matches:
   - 5 matches: 10x
   - 4 matches: 5x
   - 3 matches: 2.5x
   - 2 matches: 1.5x
   - 1 match: 0.5x
   - 0 matches: 0x (lose)
6. Winnings calculated and added to balance
7. Result announced with matches and multiplier
8. All plays logged to Discord (if enabled)

## Example Output
**5 Matches (Jackpot):**
```
🎱 5 matches (10x)! [Username] won $1000 coins! Balance: $1500
```

**3 Matches:**
```
🎱 3 matches (2.5x)! [Username] won $250 coins! Balance: $750
```

**1 Match (Partial Return):**
```
🎱 1 matches (0.5x)! [Username] won $50 coins! Balance: $450
```

**0 Matches (Loss):**
```
🎱 0 matches (0x)! [Username] won $0 coins! Balance: $400
```

**Invalid Usage:**
```
[Username], usage: !keno 10-500
```

## Installation
1. Create a new C# action in StreamerBot
2. Copy the contents of `KenoCommand.cs`
3. Set the trigger to `!keno` command
4. Ensure `ConfigSetup.cs` has been run first
5. Test with `!keno [amount]` in chat

## Tips
- Higher matches mean exponentially better payouts
- Even 1-2 matches give partial returns
- No cooldown allows repeated play
- Simple, lottery-style mechanic

---
Created by HexEchoTV (CUB) | [GitHub](https://github.com/HexEchoTV/Streamerbot-Commands)
