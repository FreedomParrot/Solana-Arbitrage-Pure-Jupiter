# Jupiter Arbitrage Bot

An automated arbitrage trading bot for Solana that uses Jupiter DEX to find and execute profitable trading opportunities. The bot continuously monitors price differences between token pairs and executes trades when profitable opportunities are detected.

## 🚀 Features

- **Automated Arbitrage Trading**: Continuously monitors and executes profitable trades
- **Pure Jupiter Strategy**: Uses your own tokens for arbitrage (no flash loans required)
- **Atomic Transactions**: All trades execute atomically to minimize risk
- **Smart Slippage Management**: Dynamic slippage adjustment based on trade size
- **Price Impact Protection**: Automatically skips trades with high price impact
- **Profit Margin Filtering**: Only executes trades that meet minimum profit thresholds
- **Cross-Platform**: Works on both Linux and Windows
- **Standalone Executables**: No Node.js installation required when using pre-built executables

## ⚠️ Important: Fee Structure

**A 15% fee is automatically deducted from all profits** and sent to the fee wallet. This fee is calculated and transferred automatically as part of each successful trade. The fee wallet address is embedded in the bot and cannot be modified.

## 📋 Prerequisites

### For Using Pre-built Executables:
- **Linux**: No additional requirements (executable is self-contained)
- **Windows**: No additional requirements (executable is self-contained)

### For Building from Source:
- **Node.js** (v18 or higher)
- **npm** or **yarn**
- **TypeScript** (installed automatically with dependencies)

## 📦 Installation

### Option 1: Using Pre-built Executables (Recommended)

1. Download the executable for your platform:
   - **Linux**: `jupiter-arb-linux`
   - **Windows**: `jupiter-arb-win.exe`

2. Make the executable executable (Linux only):
   ```bash
   chmod +x jupiter-arb-linux
   ```

3. Place your wallet keypair file (`keypair.json`) in the same directory or note its path.

### Option 2: Building from Source

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd jupiter-arb-pure-main
   ```

2. Install dependencies:
   ```bash
   npm install
   # or
   yarn install
   ```

3. Build the project:
   ```bash
   npm run build
   ```

4. Run using Node.js:
   ```bash
   npm start simple-jupiter-arb -k keypair.json -m1 <mint1> -m2 <mint2> -a <amount>
   ```

## 🔑 Wallet Setup

You need a Solana wallet keypair file to use the bot. The keypair file should be in JSON format with your private key as an array of numbers.

**Security Warning**: Never share your keypair file or commit it to version control. Keep it secure and backed up.

Example keypair structure:
```json
[123,45,67,89,...]
```

## 💻 Usage

### Linux

#### Using Pre-built Executable:
```bash
./jupiter-arb-linux simple-jupiter-arb \
  -k keypair.json \
  -m1 EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v \
  -m2 So11111111111111111111111111111111111111112 \
  -a 1000 \
  -s 600 \
  -c 10000
```

#### Using Node.js (if built from source):
```bash
node dist/index.js simple-jupiter-arb \
  -k keypair.json \
  -m1 EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v \
  -m2 So11111111111111111111111111111111111111112 \
  -a 1000 \
  -s 600 \
  -c 10000
```

### Windows

#### Using Pre-built Executable:
```cmd
jupiter-arb-win.exe simple-jupiter-arb ^
  -k keypair.json ^
  -m1 EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v ^
  -m2 So11111111111111111111111111111111111111112 ^
  -a 1000 ^
  -s 600 ^
  -c 10000
```

#### Using Node.js (if built from source):
```cmd
node dist\index.js simple-jupiter-arb ^
  -k keypair.json ^
  -m1 EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v ^
  -m2 So11111111111111111111111111111111111111112 ^
  -a 1000 ^
  -s 600 ^
  -c 10000
```

### Check Wallet Balance

**Linux:**
```bash
./jupiter-arb-linux check-balance -k keypair.json
```

**Windows:**
```cmd
jupiter-arb-win.exe check-balance -k keypair.json
```

## 📖 Command Reference

### `simple-jupiter-arb`

Performs pure Jupiter arbitrage trading between two tokens.

#### Required Options:
- `-k, --keypair <path>`: Path to your wallet keypair JSON file
- `-m1, --token-mint1 <address>`: First token mint address (e.g., USDC)
- `-m2, --token-mint2 <address>`: Second token mint address (e.g., SOL)
- `-a, --amount <number>`: Trading amount in tokens (not lamports)

#### Optional Options:
- `-p, --min-profit <number>`: Minimum profit required in tokens (default: trading amount)
- `-s, --slippage-bps <number>`: Slippage tolerance in basis points (default: 600 = 6%)
- `-c, --compute-unit-price <number>`: Compute unit price in micro-lamports (default: 10000)

#### Examples:

**Basic usage:**
```bash
# Linux
./jupiter-arb-linux simple-jupiter-arb -k keypair.json -m1 EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v -m2 So11111111111111111111111111111111111111112 -a 1000

# Windows
jupiter-arb-win.exe simple-jupiter-arb -k keypair.json -m1 EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v -m2 So11111111111111111111111111111111111111112 -a 1000
```

**With minimum profit requirement:**
```bash
# Linux
./jupiter-arb-linux simple-jupiter-arb -k keypair.json -m1 <mint1> -m2 <mint2> -a 1000 -p 10

# Windows
jupiter-arb-win.exe simple-jupiter-arb -k keypair.json -m1 <mint1> -m2 <mint2> -a 1000 -p 10
```

**With custom slippage:**
```bash
# Linux
./jupiter-arb-linux simple-jupiter-arb -k keypair.json -m1 <mint1> -m2 <mint2> -a 1000 -s 1000

# Windows
jupiter-arb-win.exe simple-jupiter-arb -k keypair.json -m1 <mint1> -m2 <mint2> -a 1000 -s 1000
```

### `check-balance`

Checks your wallet's SOL balance.

#### Required Options:
- `-k, --keypair <path>`: Path to your wallet keypair JSON file

#### Example:
```bash
# Linux
./jupiter-arb-linux check-balance -k keypair.json

# Windows
jupiter-arb-win.exe check-balance -k keypair.json
```

## 🔧 Common Token Addresses

Here are some common Solana token mint addresses you might use:

- **USDC**: `EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v`
- **SOL (Wrapped)**: `So11111111111111111111111111111111111111112`
- **USDT**: `Es9vMFrzaCERmJfrF4H2FYD4KCoNkY11McCe8BenwNYB`

You can find more token addresses on [Solana Explorer](https://explorer.solana.com/) or [Solscan](https://solscan.io/).

## 📊 Understanding the Output

When the bot is running, you'll see output like:

```
=== PURE JUPITER ARBITRAGE ===
Mint1 account: <address>
Mint2 account: <address>
Strategy: Buy Mint2 → Sell Mint2 for profit

Trading amount: 1000 tokens
Min for profit: 1000.000000 tokens
Priority fee: 10000 micro-lamports
=============================================

⚡ PROFIT! 12345 lamports (0.012345 tokens, 1.2345%) - EXECUTING...
   Start:  1000.000000
   After:  1000.012345
   Price impact: 0.1234%
   Profit margin: 123 bps
   Slippage: 600 bps (6.0%)
💰 Fee: 0.001852 tokens (15% of 0.012345 profit)

✅ SUCCESS!
https://solscan.io/tx/<transaction-id>
```

## ⚙️ Configuration Tips

### Slippage Settings
- **Small trades (< 1000 tokens)**: 600-800 bps (6-8%)
- **Medium trades (1000-5000 tokens)**: 800-1200 bps (8-12%)
- **Large trades (> 5000 tokens)**: 1200-2000 bps (12-20%)

### Compute Unit Price
- **Default**: 10000 micro-lamports (good for most cases)
- **High competition**: 50000-100000 micro-lamports (faster execution)
- **Low competition**: 5000-10000 micro-lamports (lower fees)

### Minimum Profit
Set a minimum profit threshold to avoid executing trades with very small profits that might not cover transaction fees after the 15% fee deduction.

## 🛠️ Troubleshooting

### "Cannot find module" errors
- **Solution**: If building from source, make sure you've run `npm install` or `yarn install`

### "Insufficient balance" errors
- **Solution**: Ensure your wallet has enough tokens and SOL for transaction fees

### "Slippage exceeded" errors
- **Solution**: Increase the slippage tolerance using `-s` option (try 1000-1500 bps)

### "No buy route" or "No sell route" messages
- **Solution**: The bot is working correctly but no profitable opportunities exist at the moment. It will continue monitoring.

### Transaction failures
- **Solution**: 
  - Check your SOL balance (need SOL for transaction fees)
  - Increase compute unit price with `-c` option
  - Check network connectivity
  - Verify token mint addresses are correct

### Permission denied (Linux)
- **Solution**: Make the executable executable: `chmod +x jupiter-arb-linux`

## 🔒 Security Best Practices

1. **Never share your keypair file** - Keep it secure and backed up
2. **Use a dedicated trading wallet** - Don't use your main wallet
3. **Start with small amounts** - Test with small trades first
4. **Monitor your wallet** - Keep an eye on your balance and transactions
5. **Verify token addresses** - Double-check mint addresses before trading

## 📝 Notes

- The bot runs continuously until stopped (Ctrl+C)
- All trades are atomic (all-or-nothing)
- The 15% fee is automatically calculated and deducted from profits
- The bot automatically handles token account creation if needed
- Large trades may have higher slippage requirements
- The bot includes automatic retry logic for failed transactions


## 📄 License

MIT

## ⚠️ Disclaimer

This software is provided as-is for educational and trading purposes. Trading cryptocurrencies involves risk. Always:
- Start with small amounts
- Understand the risks
- Monitor your trades
- Never invest more than you can afford to lose

The 15% fee is non-negotiable and embedded in the bot. Make sure you understand the fee structure before using the bot.

## 🆘 Support

For issues, questions, or contributions, please refer to the project repository or contact us on discord.

---

**Happy Trading! 🚀**
