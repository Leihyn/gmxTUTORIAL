# GMX V2 Tutorial

A hands-on tutorial for learning how to interact with the GMX V2 protocol through smart contract development. This project provides structured exercises covering key GMX operations including swaps, leveraged positions, liquidity provision, and more.

## Overview

This tutorial uses Foundry to provide a complete learning environment where you can:
- Build smart contracts that interact with GMX V2
- Test your implementations using mainnet forks
- Compare your solutions with reference implementations
- Learn real-world DeFi integration patterns

## Prerequisites

- [Foundry](https://book.getfoundry.sh/getting-started/installation) - Ethereum development toolkit
- Basic understanding of Solidity and smart contracts
- Familiarity with DeFi concepts (swaps, leverage, liquidity pools)
- An RPC endpoint for Arbitrum mainnet (e.g., from [Alchemy](https://www.alchemy.com/) or [Infura](https://www.infura.io/))

## Setup

1. Clone the repository:
```bash
git clone <repository-url>
cd gmxTUTORIAL
```

2. Install dependencies:
```bash
forge install
```

3. Configure environment variables:
```bash
cp .env.sample .env
```

4. Edit `.env` and add your Arbitrum RPC URL:
```
FORK_URL=https://arb-mainnet.g.alchemy.com/v2/YOUR_API_KEY
```

## Project Structure

```
.
├── src/
│   ├── exercises/          # Exercise templates to complete
│   ├── solutions/          # Reference implementations
│   ├── interfaces/         # GMX protocol interfaces
│   ├── lib/               # Helper libraries
│   └── types/             # GMX type definitions
├── test/                  # Test files for each exercise
├── exercises/             # Exercise instructions (markdown)
└── foundry.toml          # Foundry configuration
```

## Available Exercises

### Basic Operations
- **Market Swap** - Create market orders to swap tokens
- **Limit Swap** - Set up limit orders with specific price targets
- **Stake** - Stake GMX tokens and manage rewards

### Leveraged Trading
- **Long Position** - Open and manage leveraged long positions
- **Short Position** - Open and manage leveraged short positions
- **Take Profit & Stop Loss** - Implement automated risk management

### Liquidity Provision
- **GM Liquidity** - Provide liquidity to GMX markets
- **GLV Liquidity** - Interact with GMX Liquidity Vaults

### Advanced
- **Claim Funding Fees** - Collect funding fees from positions
- **App Exercises** - Build a complete vault strategy (Vault, Strategy, GmxHelper, WithdrawCallback)

## Building

Build the exercise templates:
```bash
forge build
```

Build the reference solutions:
```bash
FOUNDRY_PROFILE=solution forge build
```

## Testing

1. Get the current block number:
```bash
FORK_BLOCK_NUM=$(cast block-number --rpc-url $FORK_URL)
```

2. Run tests for a specific exercise:
```bash
forge test --fork-url $FORK_URL --fork-block-number $FORK_BLOCK_NUM --match-path test/MarketSwap.test.sol -vvv
```

3. Run tests for the solution:
```bash
FOUNDRY_PROFILE=solution forge test --fork-url $FORK_URL --fork-block-number $FORK_BLOCK_NUM --match-path test/MarketSwap.test.sol -vvv
```

Available test files:
- `test/MarketSwap.test.sol`
- `test/LimitSwap.test.sol`
- `test/Long.test.sol`
- `test/Short.test.sol`
- `test/GmLiquidity.test.sol`
- `test/GlvLiquidity.test.sol`
- `test/Stake.test.sol`
- `test/TakeProfitAndStopLoss.test.sol`
- `test/ClaimFundingFees.test.sol`
- `test/app/` - Application exercises

## How to Use This Tutorial

1. **Read the exercise instructions** in the `exercises/` directory
2. **Implement the contract** in `src/exercises/`
3. **Run the tests** to validate your implementation
4. **Compare with the solution** in `src/solutions/` if needed

### Example Workflow

```bash
# 1. Read the exercise
cat exercises/market_swap.md

# 2. Edit your implementation
vim src/exercises/MarketSwap.sol

# 3. Build
forge build

# 4. Test
FORK_BLOCK_NUM=$(cast block-number --rpc-url $FORK_URL)
forge test --fork-url $FORK_URL --fork-block-number $FORK_BLOCK_NUM --match-path test/MarketSwap.test.sol -vvv

# 5. If stuck, check the solution
cat src/solutions/MarketSwap.sol
```

## Key Concepts

### Execution Fees
GMX requires an execution fee (typically 0.1 ETH) for order processing. This fee is refunded if not fully used.

### Order Vaults
Orders are created by sending collateral and execution fees to GMX's order vault, then calling the appropriate router function.

### Price Decimals
Be aware of different decimal representations:
- Chainlink prices: 8 decimals
- Acceptable prices: 12 decimals
- USD amounts: 30 decimals
- Token amounts: varies by token (WETH: 18, USDC: 6)

### Market Keys
GMX uses market tokens (GM tokens) to identify trading pairs and liquidity pools.

## Resources

- [GMX Documentation](https://docs.gmx.io/)
- [GMX Synthetics Repository](https://github.com/gmx-io/gmx-synthetics)
- [Foundry Book](https://book.getfoundry.sh/)

## Contributing

Feel free to submit issues or pull requests to improve the tutorial exercises or documentation.

## License

This project is for educational purposes.
