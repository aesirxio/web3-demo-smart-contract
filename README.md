# AesirX demo web3 Smart Contract

## Excerpt

This is a basic web3 contract for NFT in [Concordium](https://concordium.com) using [CIS-2](https://proposals.concordium.software/CIS/cis-2.html)

## Prerrequisites

1. Set up [Rust](https://www.rust-lang.org/tools/install) in your environment.
1. Install the [Concordium Client](https://developer.concordium.software/en/mainnet/net/installation/downloads.html#concordium-client).
1. Install the [Cargo Concordium](https://developer.concordium.software/en/mainnet/smart-contracts/guides/setup-tools.html) plugin for Rust in your environment.
1. Set up and configure an account in your Concordium Client by using the command `concordium-client config import`.
1. Make sure that you have access to a public or a private node (either in Mainnet or Testnet).
1. Make sure you have enough CCD in your account.

## Deploying the smart contract

1. Build the WASM module and schema `cargo concordium build -e -o dist/a.wasm.v0001 -s dist/schema.v0001.bin` (the actual output names can change).
1. Deploy the WASM module into the Concordium network, using the account that you configured in your environment `concordium-client --grpc-ip <node ip> --grpc-port <node port> module deploy dist/a.wasm.v0001 --name aesirx_web3_demo_v0001 --sender <account address>`.
1. Initialize the smart contract in the Concordium network `concordium-client --grpc-ip <node ip> --grpc-port <node port> contract init aesirx_web3_demo_v0001 --contract aesirx_web3_demo_v0001 --sender <account address> --energy 10000` (the max NRG amount can be adjusted). This step will return an index of the deployed contract.
1. Check your smart contract using the returned index `concordium-client  --grpc-ip <node ip> --grpc-port <node port> contract show <index>`
1. Mint any NFTs using the same owner account `concordium-client  --grpc-ip <node ip> --grpc-port <node port> contract update <index> --entrypoint mint --energy 10000 --sender <account> --parameter-json dist/params001.json` (the max NRG amount can be adjusted). A sample JSON file is provided below.
1. Display your contract and tokens `concordium-client --grpc-ip <node ip> --grpc-port <node port> contract invoke <index></index> --entrypoint view`

## Example JSON file (dist/params001.json)

```json
{
  "owner": {
    "Account": ["<account>"]
  },
  "tokens": ["<lowercase hex of length 8>"]
}
```
