<h1 align="center">How to Use Oracle in Smart Contract(1)</h1>
<p align="center" class="version">Version 0.1</p>

## 1. Introduction of Ontology oracle

Blockchain Oracle is designed to solve the problem that smart contract can't interact with outside world. Now more and more dApps depend on trigger from outside world: for example:

One flight will arrive at 10:00 am. If a flight delays, an insurance smart contract will be triggered and all applicants will get 100 tokens for compensation.

Now dApps need more and more outside world data, like flight information, stock price, weather information, match result...

Ontology oracle is a role of data transporter, making it possible for a smart contract to get data from outside world.

## 2. Oracle framework

![framework](https://upload-images.jianshu.io/upload_images/150344-fe85d3ebf8c4604b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### On-chain（application & oracle contract)

On the blockchain, oracle contract receives oracle request from users and result from oracle operator. An application contract calls an oracle contract to request data from outside world and get result.

### Off-chain（oracle operator & data source）

Outside the blockchain, ontology oracle consists of oracle operator and data source.

Operator listens to the request of oracle contract in ontology network, processes the request and fetch data from data source, serialize result and then put it in oracle request.

Oracle requests consist of 2 tasks, data fetch and data parse. Data fetch gets response of target api, data parse parses the response and serialize the result according to the data structure defined by users.

![flow.png](https://upload-images.jianshu.io/upload_images/150344-4712326e94c4da2c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 3. Oracle smart contract

[the address of the source code](https://github.com/ontio/ontology-oracle/blob/master/smartcontract/oracle.py)

```python
from ontology.interop.Ontology.Contract import Migrate
from ontology.interop.System.Storage import GetContext, Get, Put, Delete
from ontology.interop.System.Runtime import CheckWitness, GetTime, Notify, Serialize, Deserialize
from ontology.interop.System.ExecutionEngine import GetExecutingScriptHash, GetScriptContainer
from ontology.interop.Ontology.Native import Invoke
from ontology.interop.System.Transaction import GetTransactionHash
from ontology.builtins import *
from ontology.interop.Ontology.Runtime import Base58ToAddress

# Global info
Admin = Base58ToAddress('AMAx993nE6NEqZjwBssUfopxnnvTdob9ij')
ONGAddress = bytearray(b'\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x02')
Fee = "Fee"
SyncAddress = "SyncAddress"
UndoRequestKey = "UndoRequest"

"""
https://github.com/ONT-Avocados/python-template/blob/master/libs/Utils.py
"""
def Revert():
    """
    Revert the transaction. The opcodes of this function is `09f7f6f5f4f3f2f1f000f0`,
    but it will be changed to `ffffffffffffffffffffff` since opcode THROW doesn't
    work, so, revert by calling unused opcode.
    """
    raise Exception(0xF1F1F2F2F3F3F4F4)

"""
https://github.com/ONT-Avocados/python-template/blob/master/libs/SafeCheck.py
"""
def Require(condition):
    """
    If condition is not satisfied, return false
    :param condition: required condition
    :return: True or false
    """
    if not condition:
        Revert()
    return True

def RequireWitness(witness):
    """
    Checks the transaction sender is equal to the witness. If not
    satisfying, revert the transaction.
    :param witness: required transaction sender
    :return: True if transaction sender or revert the transaction.
    """
    Require(CheckWitness(witness))
    return True

def Main(operation, args):
    if operation == "CreateOracleRequest":
        if len(args) != 2:
            return False
        request = args[0]
        address = args[1]
        return CreateOracleRequest(request, address)
    if operation == "SetOracleOutcome":
        if len(args) != 4:
            return False
        txHash = args[0]
        data = args[1]
        status = args[2]
        errMessage = args[3]
        return SetOracleOutcome(txHash, data, status, errMessage)
    if operation == "GetOracleOutcome":
        if len(args) != 1:
            return False
        txHash = args[0]
        return GetOracleOutcome(txHash)
    if operation == "SetFee":
        if len(args) != 1:
            return False
        fee = args[0]
        return SetFee(fee)
    if operation == "SetSyncAddress":
        if len(args) != 1:
            return False
        syncAddress = args[0]
        return SetSyncAddress(syncAddress)
    if operation == "MigrateContract":
        if len(args) !=7:
            return False
        code = args[0]
        needStorage = args[1]
        name = args[2]
        version = args[3]
        author = args[4]
        email = args[5]
        description = args[6]
        return MigrateContract(code, needStorage, name, version, author, email, description)

def CreateOracleRequest(request, address):
    #check witness
    RequireWitness(address)

    fee = Get(GetContext(), Fee)
    #transfer ong to oracle Admin address
    Require(TransferONG(address, Admin, fee))


    #get transaction hash
    txHash = GetTransactionHash(GetScriptContainer())

    #update undoRequestMap
    undoRequestMap = GetUndoRequestMap()
    undoRequestMap[txHash] = request
    b = Serialize(undoRequestMap)
    Put(GetContext(), UndoRequestKey, b)
    Notify(["createOracleRequest", request, address])
    return True

def SetOracleOutcome(txHash, data, status, errMessage):
    #check witness
    syncAddress = Get(GetContext(), SyncAddress)
    Require(len(syncAddress) == 20)
    RequireWitness(syncAddress)

    #get undoRequest map
    undoRequestMap = GetUndoRequestMap()

    #TODO : check if key exist

    #put result into storage
    result = state(data, status, errMessage)
    r = Serialize(result)
    Put(GetContext(), txHash, r)

    #remove txHash from undoRequest map
    undoRequestMap.remove(txHash)
    b = Serialize(undoRequestMap)
    Put(GetContext(), UndoRequestKey, b)
    Notify(["setOracleOutcome", txHash, status, errMessage])
    return True

def GetOracleOutcome(txHash):
    v = Get(GetContext(), txHash)
    return v

def SetFee(fee):
    RequireWitness(Admin)
    Require(fee >= 0)
    Put(GetContext(), Fee, fee)
    return True

def SetSyncAddress(syncAddress):
    RequireWitness(Admin)
    Require(len(syncAddress) == 20)
    Put(GetContext(), SyncAddress, syncAddress)
    return True

def MigrateContract(code, needStorage, name, version, author, email, description):
    RequireWitness(Admin)
    res = Migrate(code, needStorage, name, version, author, email, description)
    Require(res)
    return True

def GetUndoRequestMap():
    undoRequestMap = {}
    v = Get(GetContext(), UndoRequestKey)
    if len(v) != 0:
        undoRequestMap = Deserialize(v)
    return undoRequestMap

def TransferONG(fromAcct, toAcct, ongAmount):
    """
    transfer ONT
    :param fromacct:
    :param toacct:
    :param amount:
    :return:
    """
    RequireWitness(fromAcct)
    param = state(fromAcct, toAcct, ongAmount)
    res = Invoke(0, ONGAddress, 'transfer', [param])
    if res and res == b'\x01':
        return True
    else:
        return False
```
