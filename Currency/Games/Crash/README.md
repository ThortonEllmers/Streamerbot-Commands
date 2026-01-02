# Crash Command

## Description
A thrilling crash gambling game where users bet on when to cash out before the multiplier crashes! The game randomly determines when you'll attempt to cash out and when the game crashes - if you cash out before the crash, you win at that multiplier!

## Command
`!crash [bet amount]`

## Features
- Dynamic multiplier system (1.0x to configurable max)
- Automatic cash-out attempt generation
- Suspenseful two-message gameplay
- Detailed win/loss explanations
- Shows both crash point and cash-out timing
- Profit calculation on wins
- Better randomness with Guid-based seeding
- Configurable min/max bet and multiplier limits
- Discord logging for all crash attempts with detailed stats

## Configuration
Set in `ConfigSetup.cs`:
- `config_crash_min_bet` - Minimum bet amount (default: 10)
- `config_crash_max_bet` - Maximum bet amount (default: 500)
- `config_crash_max_mult` - Maximum multiplier (default: 10)
- `config_currency_name` - Currency name for messages
- `config_currency_key` - User variable key for balance

## Dependencies
- `ConfigSetup.cs` (must be run first to initialize all config variables)

## How It Works
1. User runs `!crash [bet]` with amount between min and max
2. Command validates bet amount and checks user balance
3. Bet is deducted from user balance
4. System generates random crash point (1.0x to max multiplier)
5. System generates random cash-out attempt point (1.0x to max multiplier)
6. First message shows bet and cash-out attempt with suspense delay
7. **If cash-out attempt < crash point**:
   - You successfully cashed out BEFORE the crash
   - WIN your bet × cash-out multiplier
   - Shows profit and total winnings
8. **If cash-out attempt > crash point**:
   - Game crashed BEFORE your cash-out attempt
   - LOSE your entire bet
   - Shows you were "too greedy"
9. Result announced with detailed explanation
10. All games logged to Discord (if enabled)

## Example Gameplay

**Starting a Game:**
```
User: !crash 100
Bot: 🎮 User bet $100 | Attempting to cash out at 3.47x...
[1.5 second suspense delay]
```

**Win (Cashed Out Before Crash):**
```
Bot: ✅ SUCCESS! | Your Cash-Out: 3.47x | Crash Point: 5.82x | Cashed out BEFORE crash! Won $347 Cub Coins (+$247 profit)! Balance: $747
```
*Explanation: You cashed out at 3.47x, and the game didn't crash until 5.82x, so you successfully cashed out before the crash and won!*

**Loss (Crashed Before Cash Out):**
```
Bot: 💥 CRASH! | Crash Point: 2.15x | Your Cash-Out: 4.23x | Game crashed BEFORE you cashed out - Too greedy! Lost $100 Cub Coins. Balance: $400
```
*Explanation: The game crashed at 2.15x, but you were trying to cash out at 4.23x, so you lost because the crash happened first - you were too greedy!*

**Insufficient Funds:**
```
User, you need $100 coins!
```

**Invalid Usage:**
```
User, usage: !crash 10-500
```

## Game Mechanics Explained

The crash game simulates a multiplier that starts at 1.0x and climbs higher and higher until it suddenly crashes. The challenge is knowing when to cash out:

- **Cash out too early**: You win, but miss out on higher multipliers
- **Cash out too late**: The game crashes before you cash out and you lose everything

In this automated version:
- The game randomly picks when it will crash (e.g., 5.82x)
- The game randomly picks when you'll try to cash out (e.g., 3.47x)
- If your cash-out timing is BEFORE the crash, you win at that multiplier
- If your cash-out timing is AFTER the crash, you lose because the game already crashed

## Understanding Win/Loss

**YOU WIN if**: Cash-out attempt < Crash point
- Example: Cash out at 3.47x, game crashes at 5.82x ✅
- You successfully cashed out before the crash

**YOU LOSE if**: Cash-out attempt > Crash point
- Example: Try to cash out at 4.23x, game crashes at 2.15x ❌
- Game crashed before you could cash out

## Installation
1. Create a new C# action in StreamerBot
2. Copy the contents of `CrashCommand.cs`
3. Set the trigger to `!crash` command with argument capture
4. Ensure `ConfigSetup.cs` has been run first
5. Test with `!crash [amount]` in chat

## Tips
- High-risk, high-reward gameplay
- Multipliers can range from 1.0x to your configured max (default 10x)
- Outcomes are purely random - no skill or strategy
- Creates exciting tension with the suspense delay
- Watch for "too greedy" messages when you lose

## Discord Logging
Logs all crash game activity including:
- Command usage with bet amounts
- Crash point and cash-out attempt values
- Win/loss results with detailed explanations
- Profit calculations on wins
- Balance changes

---
Created by HexEchoTV (CUB) | [GitHub](https://github.com/HexEchoTV/Streamerbot-Commands)
