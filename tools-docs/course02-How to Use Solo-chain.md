<h1 align="center">How to Use Solo-chain</h1>
<p align="center" class="version">Version 0.1</p>

### 1. Installation

Solo-chain is an Ontology single-node private-net. It generates a block every six seconds.

You can view the [source code](https://github.com/punicasuite/solo-chain) in GitHub and download the release version from [here](https://github.com/ontio/ontology/releases).

### 2. Introduction 

![main UI](https://upload-images.jianshu.io/upload_images/150344-62117517702035a1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

1. The function of "reboot" is to restart the private-net and clear the existing data. And the function of "stop" is to stop the private-net.
2. The default port of RPC server is 20336. For Restful server, the port is 20334. For websocket server, it is 20335.
3. The height of blockchain will increase by one every six seconds. Gas price can be changed in the setting. Gas limit is a fixed number, 20000.
4. In the account page, we have 5 accounts at first and the ONT and ONG in each account can be transferred. The ONG can be obtained by redeeming ONG.

![block page](https://upload-images.jianshu.io/upload_images/150344-bd626f2fb4abe9e1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5. The block page displays all blocks that contain transactions. 

![transaction page](https://upload-images.jianshu.io/upload_images/150344-624bce935e67d900.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

6. The transaction page displays transactions. It includes two types, deploy and invoke. You can see transaction details by clicking "Detail". 

![event page](https://upload-images.jianshu.io/upload_images/150344-e544b89d4cbb7447.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

7. The event page displays all events that are invoked by "notify" in the smart contract. 

![page of smart contract](https://upload-images.jianshu.io/upload_images/150344-9054911593dc7824.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

8. The page of smart contract displays all smart contracts that has been deployed in the blockchain.
At initialization, the blockchain will deploy several native contract by default. 

![logs page](https://upload-images.jianshu.io/upload_images/150344-b3d16350249e74b3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

9. The log page displays all log of test node at runtime.

### 3. Solo-chain demo

**Step1** - Start solo-chain 

![step 1](https://upload-images.jianshu.io/upload_images/150344-dcb35a41dce1ffa2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


**Step2** - Transfer and redeem ONG 

2.1 Transfer ONT to another account

![transfer](https://upload-images.jianshu.io/upload_images/150344-211110365df9ee33.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2.2 redeem ONG

![redeem](https://upload-images.jianshu.io/upload_images/150344-4b3359f29ee2e407.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**Step3** - Write a smart contract with SmartX

You can refer to [this document](http://punica.ont.io/tutorials/Learning-SmartX-How-to-Develop-a-dApp-with-Python-SDK/) for how to write a smart contract with SmartX.

**Step4** - Transfer 1000 ONG to Cyano wallet for deploying smart contracts.

4.1 Install Cyano wallet in Chrome, open it and create a new account.

![cyano wallet](https://upload-images.jianshu.io/upload_images/150344-585b8e0c7687b752.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


4.2 Create a new account and get public address

![new account](https://upload-images.jianshu.io/upload_images/150344-2dc15c881913de5d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![public address](https://upload-images.jianshu.io/upload_images/150344-f46765ac09c6ef8f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4.3 Transfer ONG to the new account by solo-chain

![transfer ONG](https://upload-images.jianshu.io/upload_images/150344-24ba027e878a9bce.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![balance](https://upload-images.jianshu.io/upload_images/150344-710d4931731a9776.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
Please feel free to give any suggestion
Contact: Yue Zhao 
Wechat: 16621171248
Email: messixaviinsta0303@163.com
```

