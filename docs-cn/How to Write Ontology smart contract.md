# How to Write Ontology smart contract

ontology 智能合约目前支持C#和Python两种语言编写智能合约

##Introduce

一份标准的智能合约主要有三个部分

- 头部package的引用，

- 入口处Main函数定义

- 合约具体调用函数的实现


##1.1 Package import
和其他任何编程语言一样，开发智能合约也需要在头部声明需要引用的package，

常用的package

```python
from boa.interop.System.Runtime import CheckWitness，Notify,Log
```
- CheckWitness  校验账户的权限的函数
- Notify  可以将任意格式消息推送到到blockchain

```python
from boa.interop.System.Storage import GetContext, Get, Put, Delete
```
- GetContext  获取当前区块的上下文，任何存储操作，都需要这个参数
- Put  将具体的key, value的键值对存储在合约中

关于python 智能合约的API可以访问我们的[Python API](https://github.com/ontio/neo-boa/blob/master/Ontology_smart_contract_API_for_Python.md)




##1.2 Main function define

```python

def Main(operation, args):
    if operation == 'xxx':
        p1 = args[0]
        return X(p1)

    if operation == 'Add':
        p1 = args[0]
        p2 = args[1]
        return Add(p1, p2)
```

上面的代码片段声明了合约的入口函数Main，在Main函数内部可以声明若干operation，对应具体的实际调用的函数

operation是合约外部调用的名称，必须是字符串，

比如要调用一个Add的数学操作，opertaion = "Add",
```python
if operation == 'Add':
```

通过 p1 = args[0]这样的赋值语句接收参数，N个参数相同处理。

```python
 p1 = args[0]
 p2 = args[1]
```

接收参数后，通过实际调用具体的实现函数完成合约的调用，

```python
return Invoke(p1, p2, ...pn)
```



##1.3 Function Implement

合约实际执行函数的函数和传统的编程语言一样，主要是合约逻辑处理、数据存储，并将合约执行的结果返回给Main合约即可。

下面是执行Add 操作的实现


```python
 def Add(p1, p2):
    return a + b
```

