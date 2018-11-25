<h1 align="center">How to Use Ontology Signature Service</h1>
<p align="center" class="version">Version 0.1</p>

## 1. What is Ontology signature service

A service to facilitate account management and secure signing of messages to be broadcast to the Ontology blockchain. The signature service can be used as a part of a larger application server or as it's own stand-alone microservice. It is ideal for use in applications that require a automated transaction signing in a secure hosted environment, and provides a wide range of functionality which include:

### Account
- Creation
- Exports for secure backups

### Signing
- Arbitrary data in hex string format
- Raw transactions
- Raw multiple signature transactions

### Signing (convenience methods)
- Asset transfers (eg. ONT or ONG)
- Ontology Native Smart Contract invocations
- NEO VM Smart Contract invocations w/ parameterized arguments
- NEO VM Smart Contract invocations w/ unparameterized arguments + abi

**NOTE**: The service is solely responsible for signing of the provided input with the accounts it manages. The broadcast of all signed outputs must be handled by a separate service.

## 2. How to install signature service

The signature service is a part of the [core Ontology repository](https://github.com/ontio/ontology). Download the core Ontology protocol repository and install all dependencies in the proper directory `$GOPATH/src/github.com/ontio`

```
git clone https://github.com/ontio/ontology.git
```
or
```
go get github.com/ontio/ontology
```

Navigate to the local repository
```
$GOPATH/src/github.com/ontio/ontology
```

Install project dependencies
```
glide install
```

Build SigSvr from source code
```
make tools
```

Navigate into the tools directory
```
cd tools
```

## 3. Get started

### 3.1 Start the service
To quickly get the service running with all the default options, simply run the command
```
./sigsvr
```
The service will now be accessible at:
```
http://localhost:20000/cli
```

### 3.2 Logging
Different levels of service logging available. By default, the logging level is set to Info (2). However there are seven different levels of logging available.

0. Trace
1. Debug
2. Info (default)
3. Warn
4. Error
5. Fatal
6. Max Level

For example:
```
./sigsvr --loglevel 0
```

### 3.2 Importing existing wallet data
You may already have a set of wallets generated offline, and would like to import them to the service. In order to do this, you can use the import command along with the `wallet` option to point to an existing `.dat` file to import wallets from. 

For example:
```
./sigsvr import --wallet ./wallet_2018-10-31-23-59-59.dat
```

It can be useful to import wallets from an export using the services export function.

## 4. API structure

The signature service is a JSON RPC server available by default at:
```
http://localhost:20000/cli
```
Supported request method:
```
POST
```

#### Request structure
```
{
qid: "XXX",      // Request ID. The response will echo back the same qid
method: "XXX",   // Requested method name
account: "XXX",  // Account for sign
pwd: "XXX",      // Account password
params: {}       // Input parameters for the requested method
}
```

#### Response structure
```
{
qid: "XXX",         // Request ID
method: "XXX",      // Requested method name
result: {           // Response result
signed_tx: "XXX"  // Signed transaction
},
error_code: 0,      // Error code，zero represents success, non-zero represents failure
error_info: ""      // Error description
}
```

#### Error codes

Error code | Error description
---------- | -----------------
1001       | Invalid http method
1002       | Invalid http request
1003       | Invalid request parameter
1004       | Unsupported method
1005       | Account is locked
1006       | Invalid transactions
1007       | ABI is not found
1008       | ABI is not matched
9999       | Unknown error

## 5. How to use API methods

### 5.1 Account methods

Creates a new account and adds to wallet. Note that this does not create a backup of the new account. So please be sure to use the Export Account method regularly to properly backup any newly created wallets.

**Method Name**
```
createaccount
```

**Request parameters**
```
None
```

**Response**
```
{
"account": "XXX"             // The address of account created by sigsvr
}
```

**Example**

Request:
```
{
"qid": "t",
"method": "createaccount",
"pwd": "XXXX",              // The unlock password of account created by sigsvr
"params": {}
}
```

Response:
```
{
"qid": "t",
"method": "createaccount",
"result": {
"account": "AG9nms6VMc5dGpbCgrutsAVZbpCAtMcB3W"
},
"error_code": 0,
"error_info": ""
}
```

**Method Name**
```
exportaccount
```

Export accounts method will export all accounts in wallet data into a `.dat` wallet file. This can be used to backup the accounts managed by this service.

**Request parameters**

```
{
"wallet_path": "XXX"   // Path to save .dat wallet file to. If left blank, will default to the sigsvr default path.
}
```

**Response result**

```
{
"wallet_file": "XXX"   // Full path of exported wallet file.
"account_num": "XXX"   // Number of accounts exported in the wallet file.
}
```

**Examples**

Request:
```
{
"qid": "t",
"method": "exportaccount",
"params": {}
}
```

Response:
```
{
"qid": "t",
"method": "exportaccount",
"result": {
"wallet_file": "./wallet_2018_08_03_23_20_12.dat",
"account_num": 9
},
"error_code": 0,
"error_info": ""
}
```

### 5.2 Signing Methods

#### Sign Arbitrary Data

Signs arbitrary data as long as it is encoded as a hex string.

**Method Name**
```
sigdata
```

**Request parameters**
```
{
"raw_data": "XXX"       // Unsigned data, Note that data must be encode as a hex string.
}
```

**Response result**
```
{
"signed_data": "XXX"    // Signed data, Note that data was encoded as a hex string.
}
```

**Examples**

Request:
```
{
"qid": "t",
"method": "sigdata",
"account": "XXX",
"pwd": "XXX",
"params": {
"raw_data": "48656C6C6F20776F726C64" // Hello world
}
}
```

Response:
```
{
"qid": "t",
"method": "sigdata",
"result": {
"signed_data": "cab96e...7260cb"
},
"error_code": 0,
"error_info": ""
}
```

#### Sign Raw Transaction

Signs a raw transaction.

**Method Name**
```
sigrawtx
```

**Request parameters**
```
{
"raw_tx": "XXX"      // Unsigned transaction
}
```

**Response result**
```
{
"signed_tx": "XXX"   //Signed transaction
}
```

**Examples**

Request:
```
{
"qid": "1",
"method": "sigrawtx",
"account": "XXX",
"pwd": "XXX",
"params": {
"raw_tx": "00d141...0a0000"
}
}
```

Response:
```
{
"qid": "1",
"method": "sigrawtx",
"result": {
"signed_tx": "00d141...00c6bb"
},
"error_code": 0,
"error_info": ""
}
```

### 5.3 Convenience Methods

#### Network Fees
By default, each of the following methods will use the signing account to pay the network fee.

If you would like another account will pay the network fee:

1. Specify the payer account address as an optional input parameter.
2. Use the signed output, along with the payer account, as the input for a subsequent call to the `sigrawtx` method.

#### Sign Transfer Transaction

An asset transfer from one account to another.

**Method Name**
```
sigtransfertx
```

**Request parameters**
```
{
"gas_price": XXX,  // gasprice
"gas_limit": XXX,  // gaslimit
"asset": "ont",    // asset: ont or ong
"from": "XXX",     // Payment account
"to": "XXX",       // Receipt address
"amount": "XXX"    // Transfer amount. Note that since the precision of ong is 9, it is necessary to multiply the actual transfer amount by 1000000000 when making ong transfer.
"payer": "XXX",    // (OPTIONAL) The fee payer's account address
}
```

**Response result**

```
{
"signed_tx": "XXX" // Signed transaction
}
```

**Examples**

Request:
```
{
"qid": "t",
"method": "sigtransfertx",
"account": "XXX",
"pwd": "XXX",
"params": {
"gas_price": 0,
"gas_limit": 20000,
"asset": "ont",
"from": "ATACcJPZ8eECdWS4ashaMdqzhywpRTq3oN",
"to": "AeoBhZtS8AmGp3Zt4LxvCqhdU4eSGiK44M",
"amount": "10"
}
}
```

Response:
```
{
"qid": "t",
"method": "sigtransfertx",
"result": {
"signed_tx": "00d118...efea9c"
},
"error_code": 0,
"error_info": ""
}
```

## 6. One more thing
For more details, please refer to:
- [Signature server overview](http://dev-docs.ont.io/#/docs-en/SignServer/00-overview)
- [Getting Started](http://dev-docs.ont.io/#/docs-en/SignServer/02-getting-started)
- [API Account Methods](http://dev-docs.ont.io/#/docs-en/SignServer/04-api-account-methods?id=api-account-methods)
- [Signing Methods](http://dev-docs.ont.io/#/docs-en/SignServer/05-api-signing-methods)
- [Convenience Methods](http://dev-docs.ont.io/#/docs-en/SignServer/06-api-signing-convinience-methods)

```
Please feel free to give any suggestion
Contact: Yue Zhao 
Wechat: 16621171248
Email: messixaviinsta0303@163.com
```
