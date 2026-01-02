# Bounty Command

## Description
Hunt down criminals and claim bounty rewards! A cooldown-based earning command with thematic target names and guaranteed rewards.

## Command
`!bounty`

## Features
- Guaranteed rewards (no failure chance)
- Random bounty targets (Bandit, Outlaw, Thief, Rogue, Criminal)
- Configurable reward range
- Minutes-based cooldown
- Thematic bounty hunting messages
- Discord logging for all bounty captures

## Configuration
Set in `ConfigSetup.cs`:
- `config_bounty_min_reward` - Minimum reward (default: 50)
- `config_bounty_max_reward` - Maximum reward (default: 150)
- `config_bounty_success_rate` - Not used (always succeeds)
- `config_bounty_cooldown_minutes` - Cooldown in minutes (default: 30)
- `config_currency_name` - Currency name for messages
- `config_currency_key` - User variable key for balance

## Dependencies
- `ConfigSetup.cs` (must be run first)

## How It Works
1. User runs `!bounty` command
2. Command checks cooldown (minutes since last bounty)
3. If on cooldown, displays time remaining in minutes
4. If available, randomly selects a bounty target
5. Calculates random reward between min and max
6. Adds reward to user balance
7. Sets cooldown for configured minutes
8. Announces capture with target name and reward
9. All captures logged to Discord (if enabled)

## Example Output
**Success:**
```
🎯 [Username] captured a Bandit for $127 Cub Coins! Balance: $727
```

**Cooldown Active:**
```
[Username], next bounty in 18 minutes!
```

## Bounty Targets
The command randomly selects from:
- Bandit
- Outlaw
- Thief
- Rogue
- Criminal

## Installation
1. Create a new C# action in StreamerBot
2. Copy the contents of `BountyCommand.cs`
3. Set the trigger to `!bounty` command
4. Ensure `ConfigSetup.cs` has been run first
5. Test with `!bounty` in chat

## Tips
- Bounty always succeeds, making it reliable income
- Great for viewers who want guaranteed rewards
- Adjust cooldown based on how generous you want to be
- Pairs well with other risk-based gambling commands

---
Created by HexEchoTV (CUB) | [GitHub](https://github.com/HexEchoTV/Streamerbot-Commands)
