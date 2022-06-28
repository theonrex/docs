---
slug: /sdk.erc721withquantitysignaturemintable.generate
title: Erc721WithQuantitySignatureMintable.generate() method
hide_title: true
displayed_sidebar: typescript
---

<!-- Do not edit this file. It is automatically generated by API Documenter. -->

## Erc721WithQuantitySignatureMintable.generate() method

Generate a signature that can be used to mint a dynamic NFT

**Signature:**

```typescript
generate(mintRequest: PayloadToSign721withQuantity): Promise<SignedPayload721WithQuantitySignature>;
```

## Parameters

| Parameter   | Type                                                                  | Description         |
| ----------- | --------------------------------------------------------------------- | ------------------- |
| mintRequest | [PayloadToSign721withQuantity](./sdk.payloadtosign721withquantity.md) | the payload to sign |

**Returns:**

Promise&lt;[SignedPayload721WithQuantitySignature](./sdk.signedpayload721withquantitysignature.md)&gt;

the signed payload and the corresponding signature

## Remarks

Takes in an NFT and some information about how it can be minted, uploads the metadata and signs it with your private key. The generated signature can then be used to mint an NFT using the exact payload and signature generated.

## Example

```javascript
const nftMetadata = {
  name: "Cool NFT #1",
  description: "This is a cool NFT",
  image: fs.readFileSync("path/to/image.png"), // This can be an image url or file
};

const startTime = new Date();
const endTime = new Date(Date.now() + 60 * 60 * 24 * 1000);
const payload = {
  metadata: nftMetadata, // The NFT to mint
  to: {{wallet_address}}, // Who will receive the NFT (or AddressZero for anyone)
  quantity: 2, // the quantity of NFTs to mint
  price: 0.5, // the price per NFT
  currencyAddress: NATIVE_TOKEN_ADDRESS, // the currency to pay with
  mintStartTime: startTime, // can mint anytime from now
  mintEndTime: endTime, // to 24h from now
  royaltyRecipient: "0x...", // custom royalty recipient for this NFT
  royaltyBps: 100, // custom royalty fees for this NFT (in bps)
  primarySaleRecipient: "0x...", // custom sale recipient for this NFT
};

const signedPayload = contract.signature.generate(payload);
// now anyone can use these to mint the NFT using `contract.signature.mint(signedPayload)`
```