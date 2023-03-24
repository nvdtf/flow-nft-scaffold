# Cadence NFT Scaffold

Starter template to create a new Cadence NFT project on Flow. Cadence code is from https://github.com/onflow/flow-nft

## Setup

Run Flow emulator:

```
flow emulator
```

Deploy all contracts:

```
flow dev
```

## Initializing an Account

Create new test account for the emulator. Let's call it `user1`:

```
flow accounts create
```

Initialize `user1` account:

```
flow transactions send \
  cadence/transactions/init.cdc \
  --signer user1
```

`user1` Account can now store and receive `ExampleNFT`.

## Minting

With `user1` account initialized to receive `ExampleNFT`, we can mint into the `user1` account. The minting transaction should be signed by the account that's storing the `ExampleNFT` contract. We need to pass the recipient account's address to the mint transaction. You can grab it from the initialization step above, or `flow.json`.

```
flow transactions send \
  cadence/transactions/mint.cdc \
  0xUser1Address \
  --signer exampleNFT
```

## Get NFTs in Account

Fetch the `id`s of `ExampleNFT` NFTs stored in a given account:

```
flow scripts execute \
  cadence/scripts/get_nft_ids.cdc \
  0xUser1Address
```

## Get NFT Metadata

Fetch metadata for given `ExampleNFT` id in an account:

```
flow scripts execute \
  cadence/scripts/get_nft_metadata.cdc \
  0xUser1Address \
  nft_id
```

## Tranferring NFT to Another Account

Create and initialize another account and call it `user2`:

```
flow accounts create
flow transactions send cadence/transactions/init.cdc --signer user2
```

Transfer `ExampleNFT` with given `nft_id` to `user2`:

```
flow transactions send \
  cadence/transactions/transfer.cdc \
  0xUser2Address \
  nft_id \
  --signer user1
```
