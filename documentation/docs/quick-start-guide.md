---
sidebar_position: 3
title: Quick Start Guide
---

> _To help you get started with Keysmith_

## Pre-requisites:

1. Signed NDA with Me3 -> POC: [@Jovyn Yeo](mailto:jovyn@me3.io)
1. A JS-based project:
   - Backend: Nodejs
   - Frontend: Frameworks that support server-side rendering

## Credentials

You will be furnished with the following once pre-requisite 1 has been met:

- NPM access token
- Variables to be used in the following steps of implementation
  1. `endpoint`
  1. `partnerId`

## Setup

1. Getting access to Keysmith
   - In your project, create a file named .npmrc and paste the NPM access token furnished to you
   - Add this file in your _.gitignore_ and do not commit this file
2. Run `npm i @me3technology/keysmith`
3. In your project instantiate `Me3` instance

```js title="me3.js"
import Me3 from '@me3technology/keysmith';

const CONFIG = {
    endpoint: "use endpoint provided"
    partnerId: "use partner id provided",
    redirect_uris: "https://www.me3.io/welcome"
}

// Please refer to API Specifications section for types
// Always use the same instance of Me3 object
const me3 = new Me3(CONFIG)
```

## Usage

### 1. Generate Google SSO link for users

- To begin onboarding users to Me3, you need to direct users to perform Google SSO to grant Me3 access to user's Google Drive
- `Me3.getAuthLink('http://www.example.me3.io')`
  - Args:
    - `redirectUrl`: string -> The url to redirect users to after users performs Google SSO
  - Returns:
    - string -> Google auth url

```js
import { me3 } from "./me3.js";

const authUrl = await me3.getAuthLink("https://www.example.io");
// On your clientside, please redirect the user to authUrl to perform Google SSO
```

### 2. Authenticate your Me3 instance with Me3 backend

_❗️ Pre-requisite: Step 1 completed_

- Me3 backend uses OAuth2 bearer tokens to authenticate API requests
- `Me3.getAuthToken(code, state, sessionState)`
  - Args
    - `code`: string
    - `state`: string
    - `sesssionState`: string
  - Returns
    - boolean -> Whether authentication was successful

```js
import { me3 } from "./me3.js";

// How to get the args needed
//   - From step 1: After user successfully performed Google SSO, they wouldve been redirected to your provisioned redirectURL
//   - Please extract the query parameters from appended on the url
const url = new URL("redirected-url-from-step-1");

const code = new URLSearchParams(url.code);
const state = new URLSearchParams(url.state);
const sessionState = new URLSearchParams(url.sessionState);

const success = await me3.getAuthToken(code, state, sessionState);
```

### 3. Getting Users Wallets

_❗️ Pre-requisite: Step 2 completed_

- Keysmith handles the retrieval/creation of user wallets for you
- These wallet details should be persisted in your application during the lifetime of the user's session so that they can be utilised for transaction during the user journey
- `Me3.getWallets()`
  - Returns
    - An array of users `Wallets` for all our supported chains

```js
import { me3 } from "./me3.js";

const userWallets = await me3.getWallets();
```

### 4. Transaction Signing

_❗️ Pre-requisite: Step 3 completed_

- Keysmiths handles the transaction signing for EVM-based chains
- All that is required from your end is to identify the wallet by which the user would like to transaction and construct the `Transaction` object
  - For reference on a `Transaction`: https://docs.ethers.org/v5/api/utils/transactions/

```js
import * as ethers from "ethers";

import { me3 } from "./me3.js";

// retrieve this wallet from step 3
const walletToTransaction = {
  chainName: "eth",
  walletName: "ethereum-1",
  walletAddress: "0xb8272B0eAe5B5Ea681AcB33401b33A2c2D6db351",
  secret: "0x1da6847600b0ee25e9ad9a52abbd786dd2502fa4005dd5af9310b7cc7a3b25db",
};

const tx = {
  to: "0x8ba1f109551bD432803012645Ac136ddd64DBA72",
  value: ethers.utils.parseEther("0.5"),
};

const signedTx = await me3.signTx(walletToTransaction, tx);
// signedTx can now be sent to the blockchain
```

## Sample App:

If the above is still confusing, feel free to install the following package to try out a sample app with RESTful API implemented:

:::info

```bash
npm i @me3technology/sample
```

:::
