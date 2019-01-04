<h1 align="center">How to Use Storage API in Smart Contract</h1>
<p align="center" class="version">Version 0.1</p>

## 1. Introduction

Storage API supports basic storage operation such as get, put, and delete data. 

Storage API:
* The GetContext() is used for calling storage of a smart contract.
* The GetReadOnlyContext() is used for calling storage of a smart contract. But you do not have right to put and delete any data into persistent storage area. 
* The Get() is used for getting data from storage
* The Put() is used for saving data to storage
* The Delete() is used for deleting data from storage


| API                                      | Return Value            | Description                               |
| ---------------------------------------- | -------------- | -------------------------------- |
| Storage.GetContext                   | StorageContext | Get the current storage context                       |
| Storage.GetReadOnlyContext | Read-only StorageContext | Get the current read-only storage context
| Storage.Get(StorageContext,string)       | byte[]         | Query operation, query the corresponding value by key in the persistent storage area   |
| Storage.Get(StorageContext,byte[])       | byte[]         | Query operation, query the corresponding value by key in the persistent storage area   |
| Storage.Put(StorageContext, string,string) | void       |Insert operation, inserting data as key-value format into a persistent storage area |
| Storage.Put(StorageContext, byte[],byte[]) | void       | Insert operation, inserting data as key-value format into a persistent storage area |
| Storage.Put(StorageContext, byte[],string) | void       | Insert operation, inserting data as key-value format into a persistent storage area |
| Storage.Put(StorageContext, string,byte[]) | void       | Insert operation, inserting data as key-value format into a persistent storage area |
| Storage.Put(StorageContext, string, BigInteger) | void       | Insert operation, inserting data as key-value format into a persistent storage area |
| Storage.Put(StorageContext, byte[], BigInteger) | void       | Insert operation, inserting data as key-value format into a persistent storage area |
| Storage.Delete(StorageContext, byte[])   | void           | Delete operation, delete the corresponding value by key in the persistent storage area  |
| Storage.Delete(StorageContext, string)   | void           | Delete operation, delete the corresponding value by key in the persistent storage area  |

For more details, you can view the [API-doc](http://dev-docs.ont.io/#/docs-en/DeveloperGuide/smartcontract/05-sc-api) and the [source code](https://github.com/ontio/ontology-python-compiler) here.

## 2. How to use Storage API

```
from ontology.interop.System.Storage import GetContext, Get, Put, Delete, GetReadOnlyContext
from ontology.interop.System.Runtime import Notify

def Main(operation,args):
    if operation == 'get_sc':
        return get_sc()
    if operation == 'get_read_only_sc':
        return get_read_only_sc()
    if operation == 'get_data':
        key=args[0]
        return get_data(key)
    if operation == 'save_data':
        key=args[0]
        value=args[1]
        return save_data(key, value)
    if operation == 'delete_data':
        key=args[0]
        return delete_data(key)
    return False

def get_sc():
    return GetContext()
    
def get_read_only_sc():
    return GetReadOnlyContext()

def get_data(key):
    sc=GetContext() 
    data=Get(sc,key)
    Notify(data)
    
def save_data(key, value):
    sc=GetContext() 
    Put(sc,key,value)
    
def delete_data(key):
    sc=GetContext() 
    Delete(sc,key)
```

Note1: Put, delete, and get operation should be implemented in the same contract. Otherwise, the function you run would fail to execution.

Note2: The data you save in the blockchain can be accessed by anyone.

## 3. Contributing 

```
Please feel free to give any suggestion and help us make video better!
Contact: Yue Zhao 
Wechat: 16621171248
Email: messixaviinsta0303@163.com
```
