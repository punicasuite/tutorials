ontology-java-sdk介绍
======


项目地址为：https://github.com/ontio/ontology-java-sdk

**ontology-java-sdk**是本体官方Java SDK，ontology-java-sdk是一个综合性SDK，目前支持：本地钱包管理、数字身份管理、数字资产管理、智能合约部署和调用、与节点通信等，这里主要讲解关于通过sdk与链上数字资产合约进行交互操作的介绍和演示，

首先我们需要准备三个工具：本地私有链环境（`solochain`）、用户的`Java`项目以及数字资产合约(`SmartX`)。

---


1.私有链环境
======

solochain的介绍和使用说明地址：https://punica.ont.io/docs/soloChain/#Installation

为了便于测试和开发，Ontology官方提供一个私有链环境工具solochain，简单易用，用户只需要启动该工具，就相当于启动了一个区块链，链的节点只有该用户一个。


2.用户Java项目
======
（1）引入ontology-java-sdk
------
用户Java项目，通过引入ontology-java-sdk，实现与私有链进行连接操作，与数字资产合约进行交互行为。具体操作为：在项目poml文件中加入以下代码，目的是引入sdk的JAR包，满足后续功能使用需要：
	
	<dependency>
    	<groupId>com.github.ontio</groupId>
   		<artifactId>ontology-sdk-java</artifactId>
    	<version>1.0.6</version>
	</dependency>

（2）连接私有链
------
在Java项目中，通过设置链的连接方式完成与私有链的连接，最后生成连接对象OntSdk，用于实现后续与链的交与操作，比如部署数字资产合约、合约初始化、转账、查询余额、批量转账、授权和交易等，通过此对象来完成这些功能。
   
	String ip = "http://127.0.0.1";
    String restUrl = ip + ":" + "20334";
    String rpcUrl = ip + ":" + "20336";
    String wsUrl = ip + "：" + "20335";

    OntSdk wm = OntSdk.getInstance();
    wm.setRpc(rpcUrl);
    wm.setRestful(restUrl);
    wm.setDefaultConnect(wm.getRestful());


3.数字资产合约
======
参考资料：https://smartx.ont.io

标准OEP4数字资产合约地址为：  https://github.com/tonyclarking/python-template/blob/master/OEP4Sample/OEP4Sample.py

登陆smartX需要一个钱包文件，这里提供一个钱包文件内容：
	
	{"name":"e5315938-9770-44b6-897f-5b9d765e679a","defaultOntid":"","defaultAccountAddress":"AaKoXDSxDi8DGqBxDtbehxcu4KnEiJvXvY","createTime":"2018-11-23T08:58:35.746Z","version":"1.0","scrypt":{"n":4096,"r":8,"p":8,"dkLen":64},"identities":[],"accounts":[{"address":"AaKoXDSxDi8DGqBxDtbehxcu4KnEiJvXvY","label":"e339c6fa-9cf0-4ab8-83d1-b385b65dfb0a","lock":false,"algorithm":"ECDSA","parameters":{"curve":"P-256"},"key":"I7PO2f9vZHCr1rMWKYRMxFsLFGTh/vIT+/MV5nksRG4hn5ezw8F7kBJEFEMXbDXL","enc-alg":"aes-256-gcm","hash":"sha256","salt":"UD78O129t7aKXdSiTTQjKg==","isDefault":false,"publicKey":"0320c963f95026b6cdd17f2b6679689fea235894d4c8a3a48069e1c97561591a56","signatureScheme":"SHA256withECDSA"}],"extra":null}
将此内容保存为`wallet.dat`，然后选择登陆，密码为`123456`。在smartX工具里面，创建`Python`项目，然后使用OEP4数字资产模板，编写完成之后选择编译，将编译成功后的AVM字节码存储备用。


4.数字资产功能介绍
======

（1）部署合约
------
将在smartX上编译完成的数字资产合约的AVM字节码存储起来，用于向私有链环境部署数字资产合约，具体代码如下：

    String contractCode = "0131c.....";//AVM字节码
    ontSdk.vm().setCodeAddress(Address.AddressFromVmCode(contractCode).toHexString());
    Transaction tx = ontSdk.vm().makeDeployCodeTransaction(contractCode, true, "name",
            "v1.0", "author", "email", "desp", account.getAddressU160().toBase58(),30000000L,0);
    ontSdk.signTx(tx, new Account[][]{{account}});

    Object result = ontSdk.getConnect().syncSendRawTransaction(txHex);



（2）合约初始化
------
在Ontology网络上部署的标准OEP4数字资产合约，必须先初始化合约，将合约的参数等内容写入私有链中，否则合约无法正常使用，具体代码如下：

    String result = ontSdk.neovm().oep4().sendInit(acct,account,20000,500);
    Thread.sleep(6000); //init need it work, so wait 6 seconds

    System.out.println(ontSdk.neovm().oep4().queryName());


（3）查询余额
------
标准OEP4数字资产合约定义__balanceOf__(account)方法查询账户余额的行为，具体代码如下：

      ontSdk.neovm().oep4().queryBalanceOf(account.getAddressU160().toBase58())


（4）交易转账
------
标准OEP4数字资产合约定义__transfer__(from_acct,to_acct,amount)方法执行账户之间的转账行为，语义为from_acct向账户toacct转账数值为amount的数字资产，具体代码如下：

    showBalance(ontSdk,new Account[]{account, acct});
    String txhash = ontSdk.neovm().oep4().sendTransfer(account, acct.getAddressU160().toBase58(), 1000000000, account, 20000, 500);
    Thread.sleep(6000);
    showBalance(ontSdk,new Account[]{account, acct});



（5）授权 + 查询 + 交易
------
标准OEP4数字资产合约定义__approve__(owner,spender,amount)方法执行授权行为，语义为账户owner向使用者spender授权可使用自己账户数值为amount的数字资产；定义__allowance__(owner,spender)方法执行查询授权行为，语义为查询owner向spender授权的数值，具体代码如下：
    
	 // account授权给acct1账户，额度为1000
    System.out.println(ontSdk.neovm().oep4().queryAllowance(account.getAddressU160().toBase58(), acct1.getAddressU160().toBase58()));
    String txhash0 = ontSdk.neovm().oep4().sendApprove(account, acct1.getAddressU160().toBase58(),1000000000,account,20000,500);
    Thread.sleep(6000);
    System.out.println("First check: " + ontSdk.neovm().oep4().queryAllowance(account.getAddressU160().toBase58(), acct1.getAddressU160().toBase58()));

    // acct1将account账户的数字资产交易给其他账户
    String txhash2 = ontSdk.neovm().oep4().sendTransferFrom(acct1,account.getAddressU160().toBase58(),acct1.getAddressU160().toBase58(),1000000000,account,20000,500);
    Thread.sleep(6000);
    System.out.println("Last check: " + ontSdk.neovm().oep4().queryAllowance(account.getAddressU160().toBase58(),acct1.getAddressU160().toBase58()));



（6）批量转账
------
标准OEP4数字资产合约定义__transferMulti__(args)方法执行批量转账的行为，语义为依据args的内容分批次完成转账功能，具体代码如下：
   
    showBalance(ontSdk,new Account[]{account, acct, acct1, acct2});
    Account[] accounts = new Account[]{account, acct};
    State state = new State(account.getAddressU160(), acct1.getAddressU160(),10);
    State state2 = new State(account.getAddressU160(), acct2.getAddressU160(),10);
    String txhash = ontSdk.neovm().oep4().sendTransferMulti(accounts, new State[]{state,state2},account,20000,500);
    Thread.sleep(6000);
    showBalance(ontSdk,new Account[]{account, acct, acct1, acct2});
   


