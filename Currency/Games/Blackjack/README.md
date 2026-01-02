# Interactive Blackjack Command

## Description
A fully interactive blackjack card game where users bet currency to play against the dealer. Features real-time hit/stand decisions, realistic card distribution, automatic timeout, and cooldown protection.

## Commands
- `!blackjack [bet amount]` - Start a new blackjack game
- `!blackjack hit` (or `!blackjack h`) - Draw another card
- `!blackjack stand` (or `!blackjack s`) - Stand with current hand (dealer plays)

## Features
- **Interactive Gameplay**: Players control their hand with hit/stand commands
- **10-Second Timer**: Auto-stands if player doesn't respond within 10 seconds
- **Instant 21 Win**: Automatically stands when hitting exactly 21
- **Realistic Card Distribution**: Simulates proper 52-card deck probabilities
- **Smart Dealer AI**: Dealer stands at 16 (reduced bust rate)
- **Dealer Visibility**: Shows each card dealer draws with running totals
- **Proper Card Display**: Shows A, J, Q, K for face cards
- **Soft/Hard Ace Handling**: Aces count as 11 or 1 automatically
- **Cooldown System**: Prevents spam with configurable cooldown timer
- **Non-Persistent State**: Game state clears on bot restart (balance persists)
- **Discord Logging**: Tracks all games, wins, losses, and dealer bust rates

## Configuration
Set in `ConfigSetup.cs`:
- `config_blackjack_min_bet` - Minimum bet amount (default: 25)
- `config_blackjack_max_bet` - Maximum bet amount (default: 500)
- `config_blackjack_win_mult` - Standard win multiplier (default: 2)
- `config_blackjack_cooldown_seconds` - Cooldown between games (default: 30)
- `config_currency_name` - Currency name for messages
- `config_currency_key` - User variable key for balance

## Dependencies
- `ConfigSetup.cs` (must be run first to initialize all config variables)

## How It Works

### Starting a Game
1. User runs `!blackjack [bet]` with amount between min and max
2. Command checks cooldown (if recently played, shows time remaining)
3. Command validates bet amount and checks user balance
4. Bet is deducted from user balance
5. Player draws 2 cards, dealer draws 2 cards (only 1 shown)
6. If player has 21 (blackjack), auto-wins with 2.5x payout
7. Otherwise, player has 10 seconds to choose hit or stand

### Interactive Gameplay
- **Hit**: Player draws another card
  - If total = 21: Automatically stands
  - If total > 21: Busts and loses bet
  - If total < 21: Can hit or stand again (timer resets)

- **Stand**: Player keeps current hand, dealer plays
  - Dealer hits until reaching 16 or higher
  - Each dealer card is shown with running total

- **Timeout**: If no response within 10 seconds, automatically stands

### Game Outcomes
- **Natural Blackjack (21 on first 2 cards)**: 2.5x payout
- **Player Bust (>21)**: Lose bet
- **Dealer Bust (>21)**: Win at configured multiplier
- **Player > Dealer**: Win at configured multiplier
- **Push (same total)**: Bet returned
- **Player < Dealer**: Lose bet

### Cooldown
- After each game completes, cooldown starts
- Cooldown timer shown in user-friendly format (e.g., "45s" or "2m 15s")
- Only applies to starting new games (not hit/stand actions)

## Example Gameplay

**Starting a Game:**
```
User: !blackjack 100
Bot: 🃏 User | Your hand: K, 7 = 17 | Dealer shows: 9 | Type !blackjack hit or !blackjack stand (10s timer)
```

**Hitting:**
```
User: !blackjack hit
Bot: 🃏 User drew 3 | Your hand: K, 7, 3 = 20 | Dealer shows: 9 | Type !blackjack hit or !blackjack stand (10s timer)
```

**Perfect 21:**
```
User: !blackjack hit
Bot: 🃏 User drew A | Your hand: K, 7, 3, A = 21! 🎉 PERFECT 21! Auto-standing...
```

**Standing (Dealer Plays):**
```
User: !blackjack stand
Bot: 🃏 Dealer has: 9, 8 = 17 | Dealer stands at 17
Bot: 🃏 User had 20 | Dealer ended with 17 | You win! Balance: $600
```

**Dealer Bust:**
```
User: !blackjack stand
Bot: 🃏 Dealer has: 9, 8 = 17 | Dealer hits 7 → 24
Bot: 🃏 User had 19 | Dealer ended with 24 | DEALER BUST! You win! Balance: $700
```

**Player Bust:**
```
User: !blackjack hit
Bot: 🃏 User drew K | Your hand: K, 7, 3, K = 30 | 💥 BUST! You lose $100.
```

**Timeout:**
```
User: !blackjack 100
Bot: 🃏 User | Your hand: K, 7 = 17 | Dealer shows: 9 | Type !blackjack hit or !blackjack stand (10s timer)
[10 seconds pass]
Bot: ⏱️ User, time's up! Auto-standing...
```

**Cooldown:**
```
User: !blackjack 100
Bot: User, blackjack cooldown! Wait 25s before starting a new game.
```

## Card Values
- **Ace (A)**: 11 or 1 (automatically adjusts to prevent bust)
- **2-9**: Face value
- **10, J, Q, K**: All worth 10 points

## Dealer Strategy
- Dealer hits on all totals below 16
- Dealer stands on 16 or higher
- Each dealer card shown with running total for transparency

## Installation
1. Create a new C# action in StreamerBot
2. Copy the contents of `BlackjackCommand.cs`
3. Set the trigger to `!blackjack` command with argument capture
4. Ensure `ConfigSetup.cs` has been run first
5. Test with `!blackjack [amount]` in chat
6. Test hitting and standing with `!blackjack hit` and `!blackjack stand`

## Discord Logging
Logs all blackjack activity including:
- Command usage with bet amounts
- Game wins/losses with hand details
- Dealer bust tracking with full dealer hands
- Player busts with final totals
- Cooldown warnings
- Balance changes

---
Created by HexEchoTV (CUB) | [GitHub](https://github.com/HexEchoTV/Streamerbot-Commands)
