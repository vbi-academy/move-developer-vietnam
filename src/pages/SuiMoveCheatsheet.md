---
title: The Sui move cheatsheet
description: This is the Sui move cheatsheet. It provides a quick reference guide for developers to learn and use the Sui move library effectively.
hide_table_of_contents: true
---

```Bash
# Local Sui network
# Docs: https://docs.sui.io/build/sui-local-network
# Upgrade local:
cargo install --locked --git https://github.com/MystenLabs/sui.git --branch testnet sui

# Install local validator:
sudo apt-get install libpq-dev
cargo install --locked --git https://github.com/MystenLabs/sui.git --branch main sui-test-validator
# 
# run local Sui development test validator node
RUST_LOG="consensus=off" sui-test-validator

# Open blockchain explorer in local mode: 

# Connect CLI client to local
sui client new-env --alias local --rpc http://127.0.0.1:9000
sui client switch --env local
sui client active-env # should echo "local"

# Generate address
sui client new-address ed25519

# Convert sui.keystore format to import into browser's Sui Wallet
less ~/.sui/sui_config/sui.keystore # copy the `value` needed
sui keytool convert value # result is ok to import into Sui Wallet

# Get connected Sui Client address
sui client active-address # should echo configured address

# Get some Sui from local faucet. Need to run after each local node start, as you have nothing on fresh data
sui_local_address=$(sui client active-address) ; curl --location --request POST 'http://127.0.0.1:9123/gas' --header 'Content-Type: application/json' --data-raw "{\"FixedAmountRequest\": {\"recipient\": \"$sui_local_address\"}}" 

# Display gas objects available:
sui client gas

# Test the Move package
sui move test

# Build the Move package
sui move build

# Publish the package
sui client publish --skip-dependency-verification --gas-budget=200000000 .


```