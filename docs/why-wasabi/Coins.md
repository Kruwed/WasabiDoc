---
{
  "title": "Coins",
  "description": "On the nuances of Bitcoin's coin model with unspent transaction outputs, the privacy problems and how to fix it. This is the Wasabi documentation, an archive of knowledge about the open-source, non-custodial and privacy-focused Bitcoin wallet for desktop."
}
---

# Coins

Bitcoin has an accounting model of [unspent transaction output [UTXO]](https://bitcoin.org/en/blockchain-guide#introduction).
A transaction has inputs: the coins that are being spent, and outputs: the corresponding newly created coins (unspent).
The input of a transaction has to be an unspent output of a previous transaction.
Each UTXO is the tip of the chain of links between inputs and outputs, all the way back to a [coinbase transaction](https://en.bitcoin.it/wiki/Coinbase) that pays the miner.

## Problem

#### UTXOs are not fungible

Each UTXO is a unique snowflake with a public transaction history.
For example, when Alice sends a coin to Bob, then Bob does not just have any random UTXO, but he has specifically the coin that Alice has sent him.
When Bob sends this coin to Charlie, then Charlie can check the history of the coin and see the transaction from Alice to Bob.
But due to the pseudonymity of Bitcoin, he does not necessarily find out that Alice is involved.

Further, when Alice has one non-private coin and one private coin, and she selects both of them as the inputs of a transaction, the linking of these two coins strongly suggests that the coin that was private also belongs to Alice.
This means that coin consolidation can lead to an overall decrease of privacy, especially when using an automatic coin selection algorithm.

## Wasabi's Solution

#### Manual coin labeling and selection

Contrary to many other wallets, Wasabi does not show only the total value of bitcoin in the wallet.
Rather, in both the `Send` and `CoinJoin` tabs there is a list of all the individual UTXOs.
Because Wasabi requires users to label every receiving address, the history of each coin is clear at first glance.
In order to spend a specific coin, it must be manually selected, which prevents the wrong coin from being included in the transaction.