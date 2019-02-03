<h1 align="center">How to Use PyCharm Plugin for Ontology</h1>
<p align="center" class="version">Version 0.1</p>

## 1. The supported features

1. Contract Compilation (.py)
2. Contract Deployment (TestNet / MainNet / PrivateNet)
3. Contract Invocation (Payed / PreExec)
4. Contract Debugging (Step through / Breakpoints / Variables Preview)
5. Tools for converting data type

[Project github address](https://github.com/punicasuite/pycharm-plugin-for-ontology)

## 2. Installation 

### 2.1 Install from marketplace (recommended)

Path: PyCharm Preference -> Plugins -> Input "Ontology" in the marketplace. 

![install](https://upload-images.jianshu.io/upload_images/150344-de3359ac774a4488.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 2.2 Install from disk

1. Install Node.js, by using your favorite way such as [Official Installation Package](https://nodejs.org/en/) or [Node Version Manager](https://github.com/creationix/nvm).

2. Install `Ontdev` via command line `npm install -g ontdev`

3. [Download](https://github.com/punicasuite/pycharm-plugin-for-ontology/releases) and install the plugin's jar file from disk.

1. In the **Pycharm Preferences**, search "**Plugins**".

2. In the **Plugins**, click the `Install Plugins from Disk` button and choose the file(*.zip) you download.

### 2.3 Plugins setting

1. Download [punica-init-default-box](https://github.com/punica-box/punica-init-default-box) from github to the directory of your PyCharm project.

2. Open punica-init-default-box and the setting will be imported automatically according to punica-config.json and default-config.json. 

![setting1](https://upload-images.jianshu.io/upload_images/150344-d6dd5140fb3516b2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![setting2](https://upload-images.jianshu.io/upload_images/150344-d0b7ca93312a7550.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 3. Plugins function

### 3.1 Compile

1. Right click the file you want to compile and click `compile`.

![compile](https://upload-images.jianshu.io/upload_images/150344-65ead361a01aa706.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. Compile successfully.

![result](https://upload-images.jianshu.io/upload_images/150344-2cec9e7ab18123c4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 3.2 Deploy

1. A file named `build` will be generated after compilation. Then right click the `hello_ontology.avm` and select `Deploy`. 

![deploy](https://upload-images.jianshu.io/upload_images/150344-e8a362ebd0eb8a12.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. Input contract information.

![deploy UI](https://upload-images.jianshu.io/upload_images/150344-9d082363d575d9ba.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. Deploy successfully

![result](https://upload-images.jianshu.io/upload_images/150344-4fe60cc9b735591b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 3.3 Invoke

1. After deployment, clicking the `green arrorw` to invoke the function.

![invoke](https://upload-images.jianshu.io/upload_images/150344-3296b3ae44d656b3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. Invoke successfully

![result](https://upload-images.jianshu.io/upload_images/150344-ca6c95fc24db85f2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 3.4 Tools

This plugin provides conversion between various types:
* String <=> Hex string
* Address <=> Script hash
* Number <=> Hex string
* Byte array <=> Hex string
* Endian conversion

The entry could be found via **Tools -> Ontology Tools**:

![tools](https://upload-images.jianshu.io/upload_images/150344-798a3c6f9c30f0a8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 3.5 debug

1. Set the breakpoints

![breakpoints](https://upload-images.jianshu.io/upload_images/150344-3209a3723c30792d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. Click the `green arrow` button and then click `debug` button.

![dubug](https://upload-images.jianshu.io/upload_images/150344-f925194496c0df0c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. debugger UI that can show local variables.

![debugger](https://upload-images.jianshu.io/upload_images/150344-ed1aeb038927e3b2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4. debugger panel

![panel](https://upload-images.jianshu.io/upload_images/150344-fc26d6b6d2b0e853.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

from left to right: step over, step in, force step into, step out.

## 4. Contributing 

```
Please feel free to give any suggestion and help us make video better!
Contact: Yue Zhao 
Wechat: 16621171248
Email: messixaviinsta0303@163.com
```
