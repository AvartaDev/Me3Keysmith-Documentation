---
position: 4
title: API Specifications
---

## Me3 constructor

The main class handling all of Keysmith functionalities

### Parameters

- `config`: `Me3Config`

```js
interface ME3Config {
  endpoint: string;
  partnerId: string;
  redirect_url: string;
}
```

## `getAuthLink(redirectUrl)`

This method generates Google SSO url to enable the user go perform Google SSO with Me3 to initiate the onboarding process

### Parameters

- `redirectUrl`: string

  The URL to redirect the user upon successful completion of Google SSO

### Returns

- string

  The URL you should redirect your user to perform Google SSO with Me3

## `getAuthToken(code, state, sessionState)`

This method authenticated your app's Me3 instance against Me3 servers using OAuth2. The parameters required for this method are usually appended to the redirectUrl when the user successfully completes Google SSO.

:::danger
You must call this method prior to performing wallet retrievals or transaction signing
:::

### Parameters

- `code`: string
- `state`: string
- `sessionState`: string

### Returns

None

## `getWallets()`

This method checks if the Google signed-on user has an existing Me3 recovery key in their Google Drive. If it does not have one, it undergoes the Wallet Generation process. After which, it computes the decryption of the encrypted wallets in the DApp, and returns the wallets.

### Parameters

None

### Returns

- `Wallet[]`

  List of user's `Wallet`

```js title="Example Value"
const wallets: Wallet[] = [
  {
    chainName: "eth",
    walletName: "ethereum-1",
    walletAddress: "0xb8272B0eAe5B5Ea681AcB33401b33A2c2D6db351",
    secret:
      "0x1da6847600b0ee25e9ad9a52abbd786dd2502fa4005dd5af9310b7cc7a3b25db",
  },
  {
    chainName: "Polygon",
    walletName: "3rd_Polygon",
    walletAddress: "0xb8272B0eAe5B5Ea681AcB33401b33A2c2D6db351",
    secret:
      "0x1da6847600b0ee25e9ad9a52abbd786dd2502fa4005dd5af9310b7cc7a3b25db",
  },
];
```

```js title="Model"
interface Wallet {
  chainName: string;
  walletName: string;
  walletAddress: string;
  secret: string;
}
```

## `signTx(wallet, tx)`

This method computes a signed EVM transaction payload for broadcast into EVM blockchains, based on the existing Me3 session and desired transaction parameters.

### Parameters

- `wallet`: `Wallet` interface
- `tx`: `Object`
  - Objects follow the typical web3.eth pattern of transaction objects. Please refer to https://web3js.readthedocs.io/en/v1.2.11/web3-eth.html#eth-sendtransaction for a detailed view into forming such transaction objects.

```js title="Model"
interface Wallet {
  chainName: string;
  walletName: string;
  walletAddress: string;
  secret: string;
}
```

### Returns

- string

  The string output is a transaction hash that is ready for broadcast to compatible chains.
