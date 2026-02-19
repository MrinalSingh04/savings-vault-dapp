# SavingsVault-DApp

A secure time-locked savings contract on Ethereum that allows users to
deposit ETH and withdraw it in scheduled intervals. Built with
OpenZeppelin contracts and Foundry.

------------------------------------------------------------------------

## 📋 Overview

SavingsVault is a smart contract that enables users to create
personalized savings plans. Users can deposit ETH and set up a
withdrawal schedule where funds become available in regular intervals.
This is perfect for creating disciplined savings habits, vesting
schedules, or controlled fund releases.

### Key Features

-   **Time-locked withdrawals** --- Funds unlock at fixed intervals\
-   **Custom schedules** --- Choose interval + release amount\
-   **Secure** --- Built using audited OpenZeppelin modules\
-   **Pausable** --- Emergency pause for admin\
-   **Reentrancy protected**\
-   **Owner controls** --- Adjustable max deposit

------------------------------------------------------------------------

## 🚀 Live Deployment

Link: [https://sepolia.etherscan.io/address/0xb51cCeF7C4FCc1A0063E4f27907b90f07508119E]

  Network   Address
  --------- ----------------------------------------------
  Sepolia   `0xb51cCeF7C4FCc1A0063E4f27907b90f07508119E`

------------------------------------------------------------------------

## 📦 Installation

### Prerequisites

-   Foundry
-   Git

### Setup

``` bash
git clone <your-repo-url>
cd savings-vault
forge install
forge build
```

------------------------------------------------------------------------

## 🧪 Testing

``` bash
forge test
forge test --gas-report
forge test --match-test test_Deposit -vvvv
forge test --fuzz-runs 1000
```

**Test Coverage Includes** - Deposits - Withdrawals - Multiple unlock
cycles - Admin controls - Edge cases - Access control

------------------------------------------------------------------------

## 📖 Usage

### Create Vault

``` bash
cast send <CONTRACT_ADDRESS> \
"deposit(uint256,uint256)" \
30 100000000000000000 \
--value 1ether \
--private-key <YOUR_KEY> \
--rpc-url <RPC_URL>
```

**Params** - `intervalInDays` - `releaseAmount`

------------------------------------------------------------------------

### Check Available Funds

``` bash
cast call <CONTRACT_ADDRESS> \
"availableToWithdraw(address)(uint256)" \
<YOUR_ADDRESS> \
--rpc-url <RPC_URL>
```

------------------------------------------------------------------------

### Withdraw

``` bash
cast send <CONTRACT_ADDRESS> \
"withdraw()" \
--private-key <YOUR_KEY> \
--rpc-url <RPC_URL>
```

------------------------------------------------------------------------

### Vault Details

``` bash
cast call <CONTRACT_ADDRESS> \
"getVaultDetails(address)(uint256,uint256,uint256,uint256,uint256,uint256,uint256)" \
<YOUR_ADDRESS> \
--rpc-url <RPC_URL>
```

Returns: - totalDeposited - withdrawn - startTime - interval -
releaseAmount - available - remaining

------------------------------------------------------------------------

## 🔧 Admin Commands

### Set Max Deposit

``` bash
cast send <CONTRACT_ADDRESS> \
"setMaxDeposit(uint256)" \
200000000000000000000 \
--private-key <OWNER_KEY> \
--rpc-url <RPC_URL>
```

### Pause / Unpause

``` bash
cast send <CONTRACT_ADDRESS> "pause()" --private-key <OWNER_KEY> --rpc-url <RPC_URL>
cast send <CONTRACT_ADDRESS> "unpause()" --private-key <OWNER_KEY> --rpc-url <RPC_URL>
```

------------------------------------------------------------------------

## 🏗 Deployment

### Local

``` bash
anvil

forge script script/Deploy.s.sol:DeploySavingsVault \
--rpc-url http://localhost:8545 \
--private-key <LOCAL_PRIVATE_KEY> \
--broadcast
```

### Testnet

``` bash
forge script script/Deploy.s.sol:DeploySavingsVault \
--rpc-url https://sepolia.infura.io/v3/<KEY> \
--private-key <PRIVATE_KEY> \
--broadcast \
--verify \
--etherscan-api-key <KEY> \
-vvvv
```

------------------------------------------------------------------------


## 🔒 Security

-   ReentrancyGuard
-   Ownable
-   Pausable
-   Custom errors
-   CEI pattern
-   Strict validation

------------------------------------------------------------------------

## 📊 Gas Optimizations

-   Custom errors
-   Efficient storage
-   Minimal calculations
-   View functions for free reads

------------------------------------------------------------------------

## 🚦 Error Reference

  Error                         Meaning
  ----------------------------- -------------------------
  ZeroDeposit                   Cannot deposit 0
  VaultAlreadyExists            Vault exists
  ExceedsMaxDeposit             Deposit too large
  IntervalTooShort              Interval must be ≥1 day
  InvalidReleaseAmount          Release must be \>0
  ReleaseAmountExceedsDeposit   Release \> deposit
  NoVaultFound                  Vault missing
  NothingToWithdraw             No unlocked funds
  TransferFailed                ETH transfer failed

------------------------------------------------------------------------

## 📝 Events

``` solidity
event Deposited(address indexed user, uint256 amount, uint256 interval, uint256 releaseAmount);
event Withdrawn(address indexed user, uint256 amount, uint256 remaining);
event MaxDepositUpdated(uint256 oldAmount, uint256 newAmount);
```

------------------------------------------------------------------------

## 🤝 Contributing

1.  Fork repo
2.  Create branch
3.  Commit
4.  Push
5.  PR

------------------------------------------------------------------------

## 📄 License

MIT License

------------------------------------------------------------------------

## 🙏 Credits

-   OpenZeppelin
-   Foundry
-   Ethereum community

------------------------------------------------------------------------

## 📞 Support

Open a GitHub issue for help.
