<h1 align="center">How to Use Cyano Wallet</h1>
<p align="center" class="version">Version 0.1</p>

## 1. What is Cyano wallet
Cyano Wallet is a wallet application based on the Google and Firefox plug-in Web Extension, which implements ONT ID, wallet management, and Ontology blockchain interaction, supporting and interacting with dApp at the same time.

Cyano wallet is contributed by Ontology community. You can see the [source code](https://github.com/OntologyCommunityDevelopers/cyano-wallet) in Github.

Currently supporting:
- Create wallet using mnemonic phrase
- Login with mnemonic phrase, private key, or a stored account
- ledger /Trezor support
- View balance and record
- Send ONG and ONT
- Withdraw (redeem) ONG
- Switch between networks (TestNet/MainNet/private) with TLS support
- ONT ID support
- Ontology dAPI support
- NEO and ONT address support for normal and Ledger accounts

## 2. How to install Cyano wallet

Step 1 - Open [the Cyano wallet download link](https://github.com/OntologyCommunityDevelopers/cyano-wallet/releases) and download the newest archive.zip.

Step 2 - Open Chrome Extension and click "Load unpacked" button to open archive.zip.

![step 2](https://upload-images.jianshu.io/upload_images/150344-5c47926e08c12a0e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Step 3 - Install successfully and open Cyano wallet

![step 3](https://upload-images.jianshu.io/upload_images/150344-d8b87c2a6d603789.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 3. How to use Cyano wallet

### 3.1 The basic functions of wallet

Open Cyano wallet.

![main ui](https://upload-images.jianshu.io/upload_images/150344-277197d1b48e6e63.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Click "NEW ACCOUNT" button to create new account.

![create new account](https://upload-images.jianshu.io/upload_images/150344-1c3df27751e2dfad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

View the balance of ONT and ONG.

![Screen Shot 2018-11-16 at 11.37.27 PM.png](https://upload-images.jianshu.io/upload_images/150344-1537de22f462a4c9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Click "RECEIVE" button to see your public address.

![public address](https://upload-images.jianshu.io/upload_images/150344-1baf2b912e9769d1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Click the "Setting" button in the top right corner and select the network you want to use. There are three networks available. They are the Main-Net, Test-Net, and Private-Net. I select the "PRIVATE-NET" currently. 

![network selection](https://upload-images.jianshu.io/upload_images/150344-bbad79b5fc9fc56a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 3.2 Send and transfer

Please refer to [How to Use Solo-chain](https://github.com/punicasuite/tutorials/blob/master/toolkits-docs/course02-How%20to%20Use%20Solo-chain.md) to transfer ONT and ONG to your private-net account.

We receive 1000 ONT and ONG from solo-chain now.

![transfer](https://upload-images.jianshu.io/upload_images/150344-f5085028f45f667e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Click "Send" button to send ONT or ONG to other address.

![send](https://upload-images.jianshu.io/upload_images/150344-585bb9cad72372b4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 3.3 Create a new identity

Click the "Identity" button to create a new identity.

![identity](https://upload-images.jianshu.io/upload_images/150344-c7e8a7c05c9859e6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![create identity](https://upload-images.jianshu.io/upload_images/150344-d17e8b6b8f36d623.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

A new ONT ID will be generated.

![result](https://upload-images.jianshu.io/upload_images/150344-979f49a965133fb8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 3.4 dAPI provider 

Cyano wallet is the dAPI provider that implements OEP-6 protocol. DAPI communicates with the dAPI provider first, and then the provider communicates with the blockchain. So dAPI provider takes security responsibility for developers. It greatly facilitates the development of dApp functions.

![architecture](https://upload-images.jianshu.io/upload_images/150344-44f1c519eb2d5eb3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 3.5 Use Cyano wallet with SmartX

When deploying or running a smart contract with SmartX, SmartX will open Cyano wallet automatically to require user confirmation and signature. 

Step 1 - Select the network you want to deploy or run a smart contract.

We select the private-net here.

![select network](https://upload-images.jianshu.io/upload_images/150344-a1551dadda270fb9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Step 2 - Confirm the transaction and input the password.

![confirm](https://upload-images.jianshu.io/upload_images/150344-5cd8364317db7717.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![input pwd](https://upload-images.jianshu.io/upload_images/150344-a57a9f7ef6c14c07.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

