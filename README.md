# Blockchain Testament

This is a POC contract. No production use intended.

## Table of Contents
* [Overview](#overview)
    * [Example use case](#example-use-case)
    * [Why the Blockchain](#why-the-blockchain)
* [Usage](#usage)

## Overview

ERC-1155 contract that stores imaginary FTs and adds an ability for users to issue their testaments.
Their possessions will be split per testament rules in case of confirmed death.

In general testament hold the following info:
* issuer
* inheritors and their shares
* trusted accounts (i.e. the ones trusted to announce death of the owner)

### Example use case:

![use-case](./assets/use-case.png)

[Excalidraw source](./assets/use-case.excalidraw)

### Why the Blockchain?

We could store our testaments in Postgres? It's common and cheap. Why bother?

Blockchain is distributed, thus trustless. 
Once John stores his testament, he is sure that it will work exactly the way stated in the contract.

![blockchain-network](./assets/blockchain-network.png)

[Excalidraw source](./assets/blockchain-network.excalidraw)

## Usage

1. Start local node: `npx hardhat node`

2. Deploy `Testament` contract `npx hardhat run scripts/deploy.ts --network localhost`

3. Start hardhat console `npx hardhat console --network localhost`

4. Variables set up:
```javascript
// contract address from step 2
const contractAddress = "0xe7f1725e7734ce288f8367e1bb143e90bb3f0512"
.load scripts/console-helper.js
```

5. Interact with contract:
```javascript
// transfer 1000 GOLD from contract owner to contract user
await testament.safeTransferFrom(owner, user, GOLD, 1000, [])
// check user's gold balance
await testament.balanceOf(user, GOLD)
```
