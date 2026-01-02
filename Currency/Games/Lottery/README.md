# Lottery Command

## Description
Buy a lottery ticket and try your luck! Multiple prize tiers from jackpot to small wins.

## Command
`!lottery`

## Features
- Fixed ticket cost
- 4 prize tiers with different rarities
- Jackpot (1% chance) = 5000 coins
- Big win (4% chance) = 1000 coins
- Win (10% chance) = 300 coins
- Small win (20% chance) = 150 coins
- Loss (65% chance) = 0 coins
- No cooldown (play as often as you can afford)
- Discord logging for all lottery plays

## Configuration
Set in `ConfigSetup.cs`:
- `config_lottery_min_bet` - Not used
- `config_lottery_max_bet` - Not used
- `config_lottery_jackpot_mult` - Not used
- `config_currency_name` - Currency name for messages
- `config_currency_key` - User variable key for balance

**Note**: Lottery ticket cost and prizes are hardcoded (ticket cost uses TICKET_COST constant).

## Dependencies
- `ConfigSetup.cs` (must be run first)

## How It Works
1. User runs `!lottery` command
2. Command checks if user has enough for ticket
3. Ticket cost deducted from balance
4. Roll 1-100 for prize tier
5. Award prize if won
6. Announce result with prize name and amount
7. All lottery plays logged to Discord (if enabled)

## Prize Tiers
| Prize | Chance | Payout |
|-------|--------|--------|
| JACKPOT | 1% | 5000 coins |
| BIG WIN | 4% | 1000 coins |
| WIN | 10% | 300 coins |
| SMALL WIN | 20% | 150 coins |
| LOSE | 65% | 0 coins |

**Win rate: 35%**

## Example Output
**Jackpot:**
```
🎫 [Username] won the lottery! Prize: JACKPOT - $5000 Cub Coins! Balance: $5500
```

**Win:**
```
🎫 [Username] won the lottery! Prize: WIN - $300 Cub Coins! Balance: $800
```

**Loss:**
```
🎫 [Username] didn't win. Better luck next time! Balance: $450
```

**Insufficient Funds:**
```
[Username], lottery tickets cost $[TICKET_COST] Cub Coins! You have $25.
```

## Installation
1. Create a new C# action in StreamerBot
2. Copy the contents of `LotteryCommand.cs`
3. Set the trigger to `!lottery` command
4. Ensure `ConfigSetup.cs` has been run first
5. Test with `!lottery` in chat

## Tips
- Low entry cost makes it accessible
- Jackpot is extremely rare but life-changing
- 35% win rate means frequent small wins
- No cooldown allows spam if you have funds

---
Created by HexEchoTV (CUB) | [GitHub](https://github.com/HexEchoTV/Streamerbot-Commands)
