---
description: Custom devtools tab for easier ArLocal testing and operations
---

# ArLocal Devtools

<div data-full-width="false"><figure><img src="../.gitbook/assets/Docs-Arlocal (1).png" alt=""><figcaption></figcaption></figure></div>

The new [`ArLocal`](https://github.com/textury/arlocal) Devtools allow developers to easily interact with their local or public testnet without having to run scripts to perform certain actions. The tool can be accessed by opening the browser's devtools and clicking on the `ArLocal` tab.

## Setup

Upon startup, the tool will ask you to provide some information about the arlocal gateway you want to use. After setting the gateway URL, click the refresh button to load the action sheet.

<div data-full-width="false"><figure><img src="../.gitbook/assets/Docs-Arlocal-Refresh (1).png" alt=""><figcaption></figcaption></figure></div>

## Mint testnet AR

You can mint testnet Arweave tokens that can be used like regular AR. Enter the desired amount in the input under the `Mint AR` title and click _Mint_. The tool will call the testnet to deposit AR into the currently active wallet in Wander and request the testnet to mine a block.

## Create testnet transaction

The ArLocal Devtools allow you to create new transactions with tags, a target and data. Simply set the desired fields under the `Create Transaction` title, enter your password and click _Send Transaction_. The tool will submit the transaction and request the testnet to mine a block.

## Manual block mining

You can manually request the testnet to mine a block by clicking the _Mine_ button, under the _Send Transaction_ button.
