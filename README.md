## Foundry

**Foundry is a blazing fast, portable and modular toolkit for Ethereum application development written in Rust.**

Foundry consists of:

- **Forge**: Ethereum testing framework (like Truffle, Hardhat and DappTools).
- **Cast**: Swiss army knife for interacting with EVM smart contracts, sending transactions and getting chain data.
- **Anvil**: Local Ethereum node, akin to Ganache, Hardhat Network.
- **Chisel**: Fast, utilitarian, and verbose solidity REPL.

## Documentation

https://book.getfoundry.sh/

## Usage

### Build

```shell
$ forge build
```

### Test

```shell
$ forge test
```

### Format

```shell
$ forge fmt
```

### Gas Snapshots

```shell
$ forge snapshot
```

### Anvil

```shell
$ anvil
```

### Deploy

```shell
$ forge script script/Counter.s.sol:CounterScript --rpc-url <your_rpc_url> --private-key <your_private_key>
```

### Cast

```shell
$ cast <subcommand>
```

### Help

```shell
$ forge --help
$ anvil --help
$ cast --help
```

---

## Greeting Smart Contract

`Greeter` is a simple contract that stores and returns a greeting message. You can update the message and read it back.

- Contract: `Greeting.sol`
- Name: `Greeter`
- Key functions:
  - `constructor(string _initialGreeting)` — sets the initial greeting
  - `setGreeting(string _newGreeting)` — updates the greeting
  - `greet() → string` — reads the current greeting

### Quickstart

```bash
# Install Foundry if you haven't already
curl -L https://foundry.paradigm.xyz | bash
foundryup

# Initialize a Foundry project (if needed)
forge init

# Compile the contract
forge build
```

### Deploying `Greeter`

You can deploy using Foundry CLI or Remix IDE. Choose your preferred method below.

#### Option 1: Deploy with Remix IDE

1. **Open Remix**: Go to [remix.ethereum.org](https://remix.ethereum.org)

2. **Create a new file**: 
   - Click "Create new file" in the File Explorer
   - Name it `Greeter.sol`

3. **Copy the contract code**:
   ```solidity
   // SPDX-License-Identifier: UNLICENSED
   pragma solidity ^0.8.13;

   contract Greeter {
       string public greeting;
       constructor (string memory _initialGreeting){
           greeting = _initialGreeting;
       }
       function setGreeting (string memory _newGreeting) public{
           greeting = _newGreeting;
       }
       function greet() public view returns(string memory){
           return greeting;
       }
   }
   ```

4. **Compile the contract**:
   - Go to the "Solidity Compiler" tab
   - Select compiler version `0.8.13` or higher
   - Click "Compile Greeter.sol"

5. **Deploy the contract**:
   - Go to the "Deploy & Run Transactions" tab
   - Select your environment (Injected Provider for MetaMask, or VM for local testing)
   - In the "Constructor Arguments" field, enter: `"Hello, world!"`
   - Click "Deploy"

6. **Interact with the contract**:
   - After deployment, you'll see the contract in the "Deployed Contracts" section
   - Click on `greet` to read the current greeting
   - Use `setGreeting` to update the greeting (enter new message and click the function)

#### Option 2: Deploy with Foundry CLI

You can deploy locally to Anvil or to a testnet/mainnet by providing your RPC URL and private key. The example below shows both.



Testnet/Mainnet:

```bash
export RPC_URL="https://<your_rpc_provider>"
export PRIVATE_KEY="0x..."
forge create Greeting.sol:Greeter \
  --rpc-url $RPC_URL \
  --private-key $PRIVATE_KEY \
  --constructor-args "Hello, world!"
```

After deployment, you will get the contract address in the output. To read the greeting:



To update the greeting:

```bash
cast send <DEPLOYED_ADDRESS> "setGreeting(string)" "GM" --rpc-url $RPC_URL --private-key $PRIVATE_KEY
```
