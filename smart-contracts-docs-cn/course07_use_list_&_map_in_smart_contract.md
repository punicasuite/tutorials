<h1 align="center">How to Use List and Map in Smart Contract</h1>
<p align="center" class="version">Version 0.1</p>

## 1. How to use list

List: The most basic data structure in Python is the sequence.

Contract about list operation
```
from ontology.interop.System.Storage import Put, Get, GetContext
from ontology.interop.System.Runtime import Notify, Serialize, Deserialize
from ontology.builtins import append, remove, range, len, print

LISTKEY = "List"

def Main(operation, args):
    if operation == "init":
        return init()
    if operation == "add_list":
        elements = args[0]
        return add_list(elements)
    if operation == "remove_list":
        element = args[0]
        return remove_list(element)
    
def init():
    # init list
    list1 = [1,2,3]
    list1Info = Serialize(list1)
    # save data 
    Put(GetContext(), LISTKEY, list1Info)
    
    Notify(["init list is ",list1])
    
    return True

def add_list(elements):
    # get data from persistent storage area
    list1Info = Get(GetContext(), LISTKEY)
    list1 = Deserialize(list1Info)
    
    Notify(["before add, list is ", list1])

    for element in elements:
        list1.append(element)
    list1Info = Serialize(list1)
    Put(GetContext(), LISTKEY, list1Info)
    Notify(["after add, list is ", list1])

    return list1

def remove_list(element):
    # get data from persistent storage area
    list1Info = Get(GetContext(), LISTKEY)
    list1 = Deserialize(list1Info)
    
    Notify(["before add, list is ", list1])

    list1.remove(element)
    list1Info = Serialize(list1)
    Put(GetContext(), LISTKEY, list1Info)
    Notify(["after remove, list is ", list1])
    return list1
```

## 2. How to use map

Contract about map operation 

```
from ontology.interop.System.Storage import Put, Get, GetContext
from ontology.interop.System.Runtime import Notify, Serialize, Deserialize
from ontology.builtins import append, remove

MAPKEY = "Map"

def Main(operation, args):
    if operation == "init":
        return init()
    if operation == "add_map":
        key = args[0]
        value = args[1]
        return add_map(key, value)
    if operation == "remove_map":
        key = args[0]
        return remove_map(key)
    return False

def init():
    # init map
    map1 = {
        "key1":1,
        "key2":2
    }
    map1Info = Serialize(map1)
    Put(GetContext(), MAPKEY, map1Info)
    # return result
    Notify(["init map is ", map1["key1"], map1["key2"]])

    return True


def add_map(key, value):
    map1Info = Get(GetContext(), MAPKEY)
    map1 = Deserialize(map1Info)

    Notify(["before add, map is ", map1["key1"], map1["key2"]])
    # add data 
    map1[key] = value
    map1Info = Serialize(map1)
    Put(GetContext(), MAPKEY, map1Info)
    Notify(["after add, map is ", map1["key1"], map1["key2"], map1[key]])

    return True
    
def remove_map(key):
    map1Info = Get(GetContext(), MAPKEY)
    map1 = Deserialize(map1Info)
    Notify(["before remove, map is ", map1["key1"], map1["key2"], map1[key]])
    map1.remove(key)
    map1Info = Serialize(map1)
    Put(GetContext(), MAPKEY, map1Info)
    Notify(["after remove, map is ", map1["key1"], map1["key2"]])

    return True
```

## 3. Contributing 

```
Please feel free to give any suggestion and help us make video better!
Contact: Yue Zhao 
Wechat: 16621171248
Email: messixaviinsta0303@163.com
```
