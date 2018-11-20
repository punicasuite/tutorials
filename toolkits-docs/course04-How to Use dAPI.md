<h1 align="center">How to Use dAPI</h1>
<p align="center" class="version">Version 0.1</p>

[**Click here to view the course video**](https://drive.google.com/open?id=19H6C0_aEjKfJn_WeqsNTZtceWB4O20a2)

## 1. What is dAPI

DAPI (Decentralized API) is API for dApps on Ontology blockchain. This is an implementation of dAPI from [**OEP-6**](https://github.com/backslash47/OEPs/blob/oep-dapp-api/OEP-6/OEP-6.mediawiki) communication protocol. dApp developers can call the dAPI interface to interact with the Ontology blockchain and Chrome plug-in wallet, supporting query chain information, assets, digital identities, smart contracts, and more.

The library is written in TypeScript, so all the methods and objects are typed. It is therefore usable in TypeScript projects as well as JavaScript projects.

Features:
- The security issue of dApps is transferred to the dAPI provider. Users do not have to worry about security issues such as assets when they are in dApps.
- The interface is easy to integrate.

Note: It is necessary to have installed suitable **dAPI provider** . Reference implementation is [How to Use Cyano Wallet](https://github.com/punicasuite/tutorials/blob/master/toolkits-docs/course03-How%20to%20Use%20Cyano%20Wallet.md).

## 2. OEP-6 architecture 

The interaction between dApp and Ontology network can be described with this diagram:

![architecture](https://upload-images.jianshu.io/upload_images/150344-ec4859be6d4273f3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Yellow colored components are external to OEP-6 proposal.

Green colored components represent **dAPI.js**. It is universal implementation of communication channel for direct use by dApp developers in web browsers.

Blue colored components belong to specific implementation of dAPI provider. The implementation is out of scope of this proposal, but the implementator must adhere to the protocol used by dAPI.js.

The communication protocol has RPC style of communication. The RPC is modeled on top of standard WebExtension message passing using `runtime.sendMessage` and `runtime.onMessage.addListener`. All the complications of WebExtension is hidden for both the **dApp** and **dAPI provider** when using dAPI.js.

dAPI providers might use dAPI.js as the communication protocol, but they can also implement different protocols suitable for the specific environment (e.g: iOS, Android, Desktop).

## 3. How to install and use dAPI

### 3.1 Setting up the development environment

Please ensure you have the following installation and configuration in order to setup the development environment.

- [Node.js v6+ LTS with npm](https://nodejs.org/en/)
- [Cyano Wallet](https://chrome.google.com/webstore/detail/ontology-web-wallet/dkdedlpgdmmkkfjabffeganieamfklkm)
- [Git](https://git-scm.com/)

### 3.2 dAPI installation
The Ontology dAPI is the core API used to interface with the Ontology blockhain when creating a dApp and the repository can be found [here](https://github.com/ontio/ontology-dapi). First you must install the npm package using: 

```
$ npm install ontology-dapi
```

### 3.3 dAPI instantiation

To use the dAPI in your project, you need to import the library and then register as a client.
Import and register the dAPI using:

```
import { client } from 'ontology-dapi';

client.registerClient({});
```

### 3.4 Example dAPI methods

Once imported and registered, use the provided dAPI methods in your dApp (see below).

#### Example blockchain methods

```
const network = await client.api.network.getNetwork();
const height = await client.api.network.getBlockHeight();
const block = await client.api.network.getBlock({ block: 1 });
const transaction = await client.api.network.getTransaction({txHash: '314e24e5bb0bd88852b2f13e673e5dcdfd53bdab909de8b9812644d6871bc05f'});
const balance = await client.api.network.getBalance({ address: 'AcyLq3tokVpkMBMLALVMWRdVJ83TTgBUwU' });
```

#### Example asset methods

```
const result = await client.api.asset.makeTransfer({ recipient, asset, amount });
```

#### Example Smart Contract Methods

```
const result = await client.api.smartContract.invoke({contract,method,parameters,gasPrice,gasLimit,requireIdentity});
const result = await client.api.smartContract.invokeRead({ contract, method, parameters });
const result = await client.api.smartContract.deploy({code,name,version,author,email,description,needStorage,gasPrice,gasLimit});
```
#### Example Message Methods

```
const message: string = values.message;
const signature: Signature = {
data,
publicKey
};
const result = await client.api.message.signMessage({ message });
const result = await client.api.message.verifyMessage({ message, signature });
```

A full list of methods can be found in the [dAPI Specification document](https://github.com/backslash47/OEPs/blob/oep-dapp-api/OEP-6/OEP-6.mediawiki).


## 4. Running the demo project

Clone the [dAPI demo](https://github.com/OntologyCommunityDevelopers/ontology-dapi-demo) which we will use to demonstrate functionality.

```
git clone https://github.com/OntologyCommunityDevelopers/ontology-dapi-demo.git

cd ontology-dapi-demo

npm install

npm run start
```

The code will start the demo which can be accessed using the Google Chrome browser at http://localhost:3000.

By selecting Provider->GetProvider, you can get the info of dAPI provider.

![dApp Demo Provider](http://upload-images.jianshu.io/upload_images/150344-efd27ba3beb1ea3d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![dApp Demo Get Provider](http://upload-images.jianshu.io/upload_images/150344-bfbd5b11e8346f0f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

The function of the network allows us to communicate with the Ontology Blockchain and make API calls.  For example, We can get the following result by selecting Network->Get Block.

![dApp Demo getBlock](http://upload-images.jianshu.io/upload_images/150344-2c2c5f1cfe35faf9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

You can also initiate a transfer by selecting Asset->Make Transfer where you'll be automatically prompted to approve the transaction by Cyano Wallet. Click Confirm to approve the transaction.

![Cyano Wallet Confirm](http://upload-images.jianshu.io/upload_images/150344-b36e69f45bcf25c7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
Please feel free to give any suggestion
Contact: Yue Zhao 
Wechat: 16621171248
Email: messixaviinsta0303@163.com
```
