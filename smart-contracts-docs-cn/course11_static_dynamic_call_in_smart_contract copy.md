<h1 align="center">Static and Dynamic Application Call in Smart Contract</h1>
<p align="center" class="version">Version 0.1</p>

## 1. Introduction

| API                          | Return Value  | Description                                       |
| ---------------------------- | ---- | ---------------------------------------- |
| RegisterAppCall | function |  call a smart contract statically |
|DynamicAppCall | depend on the calling function |call a smart contract dynamically |

For more details, you can view the [API-doc](http://dev-docs.ont.io/#/docs-en/DeveloperGuide/smartcontract/05-sc-api) and the [source code](https://github.com/ontio/ontology-python-compiler) here.

## 2. Static call

The contract A

```
from boa.interop.System.App import RegisterAppCall
from boa.interop.System.Runtime import Notify

HelloWorld = RegisterAppCall('5e8d6fddb980bd5b118c45d3ebff5c5f220fa2de', 'operation', 'args')

def Main(operation, args):
    if operation == "CallHello":
        msg=args[0]
        return CallHello(msg)
    return False


def CallHello(msg):
    return HelloWorld("Hello", [msg])
```

The "Hello World " contract B invoked by contract A

```
from boa.interop.System.Runtime import Notify

def Main(operation, args):
    if operation == 'Hello':
        msg = args[0]
        return Hello(msg)

    return False


def Hello(msg):
    return msg
```

## 3. Dynamic call

The contract A

```
from boa.interop.System.App import RegisterAppCall, DynamicAppCall
from boa.interop.System.Runtime import Log, Notify


CallContract = RegisterAppCall('5e8d6fddb980bd5b118c45d3ebff5c5f220fa2de', 'operation', 'args')
# dea20f225f5cffebd3458c115bbd80b9dd6f8d5e

def Main(operation, args):
    if operation == "DynamicCallContract":
        if len(args) != 3:
            return False
        revesedContractAddress = args[0]
        opt = args[1]
        params = args[2]
        return DynamicCallContract(revesedContractAddress, opt, params)
    if operation == "StaticCallContract":
        opt = args[0]
        params = args[1]
        return StaticCallContract(opt,params)

    return False

def DynamicCallContract(revesedContractAddress, operation, params):
    res = DynamicAppCall(revesedContractAddress, operation, params)
    Notify(["the result of the DynamicCall is: ", res])
    return res

def StaticCallContract(opt, params):
    res=CallContract(opt, params)
    Notify(["the result of the StaticCall is: ", res])
    return res
```

The "Hello World " contract B invoked by contract A

```
from boa.interop.System.Runtime import Notify

def Main(operation, args):
    if operation == 'Hello':
        msg = args[0]
        return Hello(msg)

    return False


def Hello(msg):
    return msg
```
