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

You can deploy locally to Anvil or to a testnet/mainnet by providing your RPC URL and private key. The example below shows both.

Local (Anvil):

```bash
anvil
# In a new terminal window/tab
forge create Greeting.sol:Greeter \
  --rpc-url http://127.0.0.1:8545 \
  --private-key <anvil_private_key> \
  --constructor-args "Hello, world!"
```

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

```bash
cast call <DEPLOYED_ADDRESS> "greet()(string)"
```

To update the greeting:

```bash
cast send <DEPLOYED_ADDRESS> "setGreeting(string)" "GM" --rpc-url $RPC_URL --private-key $PRIVATE_KEY
```
