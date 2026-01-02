# Plinko Command

## Description
Drop a ball down the plinko board! Land in different slots for varying multipliers.

## Command
`!plinko [bet amount]`

## Features
- 11 slots with different multipliers (0x to 5x)
- Bell curve distribution (favors middle slots)
- Edge slots have extreme multipliers (0x and 5x)
- Middle slots have moderate returns
- Realistic plinko physics simulation
- Configurable min/max bet limits
- Discord logging for all plinko plays

## Configuration
Set in `ConfigSetup.cs`:
- `config_plinko_min_bet` - Minimum bet amount (default: 10)
- `config_plinko_max_bet` - Maximum bet amount (default: 500)
- `config_plinko_max_mult` - Maximum multiplier (default: 5)
- `config_currency_name` - Currency name for messages
- `config_currency_key` - User variable key for balance

## Dependencies
- `ConfigSetup.cs` (must be run first)

## How It Works
1. User runs `!plinko [bet]` with amount between min and max
2. Command validates bet amount and checks user balance
3. Bet is deducted from user balance
4. Ball starts in middle position (slot 5)
5. Ball bounces 8 times, randomly left or right each time
6. Final position determines multiplier
7. Winnings calculated based on slot multiplier
8. Result announced with slot number and outcome
9. All plays logged to Discord (if enabled)

## Slot Multipliers
```
[0x] [0.5x] [1x] [2x] [3x] [5x] [3x] [2x] [1x] [0.5x] [0x]
  0     1     2    3    4    5    6    7    8     9    10
```
**Slot 5 (center)**: 5x jackpot
**Slots 4,6**: 3x
**Slots 3,7**: 2x
**Slots 2,8**: 1x (break even)
**Slots 1,9**: 0.5x (half back)
**Slots 0,10**: 0x (lose all)

## Example Output
**Jackpot (Slot 5):**
```
🔻 [Username] dropped to slot 5 (5x) and WON $400 coins! Balance: $900
```

**Win:**
```
🔻 [Username] dropped to slot 4 (3x) and WON $200 coins! Balance: $700
```

**Break Even:**
```
🔻 [Username] dropped to slot 2 (1x) and LOST $0 coins! Balance: $500
```

**Loss:**
```
🔻 [Username] dropped to slot 0 (0x) and LOST $100 coins! Balance: $400
```

## Installation
1. Create a new C# action in StreamerBot
2. Copy the contents of `PlinkCommand.cs` (note: filename is PlinkCommand.cs, not PlinkoCommand.cs)
3. Set the trigger to `!plinko` command
4. Ensure `ConfigSetup.cs` has been run first
5. Test with `!plinko [amount]` in chat

## Tips
- Bell curve makes center slots more likely
- Jackpot (5x) is rare but possible
- Edge slots (0x) are least likely
- Realistic plinko simulation with physics

---
Created by HexEchoTV (CUB) | [GitHub](https://github.com/HexEchoTV/Streamerbot-Commands)
