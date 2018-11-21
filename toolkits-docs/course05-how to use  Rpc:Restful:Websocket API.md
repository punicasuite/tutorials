<h1 align="center">How to Use  Rpc/Restful/Websocket API</h1>
<p align="center" class="version">Version 0.1</p>

## 1. The introduction of Ontology-API

Rpc API: [http://dev-docs.ont.io/#/docs-en/API/01-rpc_api](http://dev-docs.ont.io/#/docs-en/API/01-rpc_api)

Restful API: [http://dev-docs.ont.io/#/docs-en/API/02-restful_api](http://dev-docs.ont.io/#/docs-en/API/02-restful_api)

Websocket API: [http://dev-docs.ont.io/#/docs-en/API/03-websocket_api](http://dev-docs.ont.io/#/docs-en/API/03-websocket_api)

## 2. How to use restful API in SmartX

Toolkit introduction:

![toolkit](https://upload-images.jianshu.io/upload_images/150344-593412abecfa07d6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Open [SmartX](https://smartx.ont.io), create a python project and select "Hello World" template.

![create a project](https://upload-images.jianshu.io/upload_images/150344-a08749d48d531c15.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Click the "Restful" button on the panel and then enter the "Restful" panel.

![restful panel](https://upload-images.jianshu.io/upload_images/150344-0389bc3299f76664.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

There are 23 restful APIs. You can select the network and then use the API. For example, we select Main-Net and click "Send" button of the first API. Then we receive the result as shown below.

![First API](https://upload-images.jianshu.io/upload_images/150344-197877f75b2ab565.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 3. The Rpc API in Python SDK

You can get the code of Rpc API at the following address.

Rpc code: [https://github.com/ontio/ontology-python-sdk/blob/master/ontology/rpc/rpc.py](https://github.com/ontio/ontology-python-sdk/blob/master/ontology/rpc/rpc.py)

Request parameter description:

![request](https://upload-images.jianshu.io/upload_images/150344-c38176062b7cefc4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Response parameter description:

![response](https://upload-images.jianshu.io/upload_images/150344-d94fc1e6b79688e1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

For example, If you call the "getbestblockhash" API, the following request will be sent.

```
{
"jsonrpc": "2.0",
"method": "getbestblockhash",
"params": [],
"id": 1
}
```

And you will receive the following response.

```
{
"desc":"SUCCESS",
"error":0,
"jsonrpc": "2.0",
"id": 1,
"result": "773dd2dae4a9c9275290f89b56e67d7363ea4826dfd4fc13cc01cf73a44b0d0e"
}
```

If the execution fails, you will receive the error code.

Error code instruction

| Field | Type | Description |
| :--- | :--- | :--- |
| 0 | int64 | SUCCESS |
| 41001 | int64 | SESSION\_EXPIRED: invalided or expired session |
| 41002 | int64 | SERVICE\_CEILING: reach service limit |
| 41003 | int64 | ILLEGAL\_DATAFORMAT: illegal dataformat |
| 41004 | int64 | INVALID\_VERSION: invalid version |
| 42001 | int64 | INVALID\_METHOD: invalid method |
| 42002 | int64 | INVALID\_PARAMS: invalid params |
| 43001 | int64 | INVALID\_TRANSACTION: invalid transaction |
| 43002 | int64 | INVALID\_ASSET: invalid asset |
| 43003 | int64 | INVALID\_BLOCK: invalid block |
| 44001 | int64 | UNKNOWN\_TRANSACTION: unknown transaction |
| 44002 | int64 | UNKNOWN\_ASSET: unknown asset |
| 44003 | int64 | UNKNOWN\_BLOCK: unknown block |
| 45001 | int64 | INTERNAL\_ERROR: internel error |
| 47001 | int64 | SMARTCODE\_ERROR: smartcode error |

## 4. How to use Rpc API in Python SDK

1. Install Ontology Python SDK

```
pip install ontology-python-sdk
```

2. Import Ontology package

```
from ontology.ont_sdk import OntologySdk
```

3. Initialize the instance and set up the Rpc Address

Now, we use the Private-Net. So we set Rpc address to http://127.0.0.1:20336.

```
sdk = OntologySdk()
rpc_address = 'http://127.0.0.1:20336'
sdk.rpc.set_address(rpc_address)
```

4. Call Rpc API

```
version = sdk.rpc.get_version()
count = sdk.rpc.get_node_count()
print(version)
print(count)
```

5. Result

```
v1.0.5
1
```



