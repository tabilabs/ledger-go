# ledger-go

Helper library for implementing Ledger support in the Tabi CLI. This wraps [Ledger-Go](https://github.com/tabilabs/ledger-go) to provide
a Ledger interface that is compatible (with minor additions) with the Cosmos SDK.

## Overview

Ledger-Go provides a Cosmos SDK Ledger object which can be instantiated, stored in the keyring, and used to sign CLI functions (such as sending tokens or staking) via Ledger.

## Usage

1. Create a Cosmos SDK `EncodingConfig` with the requisite type registration (e.g. using an app's `ModuleBasics`)
2. Call `TabiLedgerDerivation` using this config as a parameter to receive a `LedgerDerivation` function
3. Instantiate the Cosmos SDK Ledger instance with the provided `LedgerDerivation` function

## Technical Notes

The Ledger will take a signature byte stream of either Amino (legacy) or Protobuf type payloads, decode the payload using the provided `EncodingConfig`,
construct an EIP-712`TypedData` payload to be signed with the Ethereum Ledger app, and return the signature.
