# AR 复制 & 粘贴（原文是英文，这个不是翻译）

[视频Demo](https://www.bilibili.com/video/BV1dA411q7o5)。
[提前须知](https://blog.csdn.net/one_hwx/article/details/106611103)

该原型拥有3个独立的模块，分别是手机端APP、本地服务器和目标检测及背景移除服务。

## 模型

- **移动设备app**

  - [/app](/app)文件夹有说明app(expo)具体操作.

- **本地服务器**

  - 处理手机app和photoshop交互.
  - 关于如何摄像头定位使用到的代码在 [screenpoint](https://github.com/cyrildiagne/screenpoint)
  - 到 [/server](/server) 文件夹查看详细配置服务器步骤

- **目标检测/背景移除功能**

  - 使用 [/basnet-http](/basnet-http)

## 搭建过程
过程总结: 1.配置photoshop-> <br/>
2.学会使用[expo](https://expo.io/learn)-> <br/>
3.学会使用[BASNet-HTTP wrapper](https://github.com/cyrildiagne/basnet-http)-> <br/>
4.搭建运行服务器-> <br/> 
5.搭建运行app(通过expo启动)

### 1 - 配置 Photoshop

- 点击 "Preferences > Plug-ins",打勾 "Remote Connection" 然后设置一个密码(我用123456).
![photoShopSetting](https://github.com/122537067/ar-cutpaste/blob/master/readmeImg/photoshopSetting.png)  

- photoshop的配置应该与 ```server/src/ps.py``` 保持一致, 否则粘贴不了图层到photoshop.

- 而且要确保有一个图层背景. 


### 2 设置本地服务器

```bash
cd server
virtualenv venv
source venv/bin/activate
pip3 install -r requirements.txt
``` 
- 这里需要注意:原文使用pip install -r requirements.txt,但当你的电脑同时存在python2 和 python3 会混淆（特别是macOS）


### 2 - 设置外部突出对象检测功能

####  设置基于个人服务器的检测功能 (requires a CUDA GPU)

- 使用[BASNet-HTTP wrapper](/basnet-http) (requires a CUDA GPU)
![Docker](https://github.com/122537067/ar-cutpaste/blob/master/readmeImg/dockerMsg.png)

### 3 - 配置和运行本地服务器

- 文件夹 [/server](/server) 有说明过程.

### 4 - 配置和运行app

- 文件夹 [/app](/app) 有说明过程.

<br/><br/><br/><br/>
___
以下原文
___
# AR Cut & Paste

An AR+ML prototype that allows cutting elements from your surroundings and pasting them in an image editing software.

Although only Photoshop is being handled currently, it may handle different outputs in the future.

Demo & more infos: [Thread](https://twitter.com/cyrildiagne/status/1256916982764646402)

⚠️ This is a research prototype and not a consumer / photoshop user tool.

**Update 2020.05.11:** If you're looking for an easy to use app based on this research, head over to https://arcopypaste.app

## Modules

This prototype runs as 3 independent modules:

- **The mobile app**

  - Check out the [/app](/app) folder for instructions on how to deploy the app to your mobile.

- **The local server**

  - The interface between the mobile app and Photoshop.
  - It finds the position pointed on screen by the camera using [screenpoint](https://github.com/cyrildiagne/screenpoint)
  - Check out the [/server](/server) folder for instructions on configuring the local server

- **The object detection / background removal service**

  - For now, the salience detection and background removal are delegated to an external service
  - It would be a lot simpler to use something like [DeepLap](https://github.com/shaqian/tflite-react-native) directly within the mobile app. But that hasn't been implemented in this repo yet.

## Usage

### 1 - Configure Photoshop

- Go to "Preferences > Plug-ins", enable "Remote Connection" and set a friendly password that you'll need later.
- Make sure that your PS document settings match those in ```server/src/ps.py```, otherwise only an empty layer will be pasted.
- Also make sure that your document has some sort of background. If the background is just blank, SIFT will probably not have enough feature to do a correct match.

<!--
### 2) Setup the local server

```bash
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
``` -->

### 2 - Setup the external salience object detection service

#### Option 1: Set up your own model service (requires a CUDA GPU)

- As mentioned above, for the time being, you must deploy the
BASNet model (Qin & al, CVPR 2019) as an external HTTP service using this [BASNet-HTTP wrapper](https://github.com/cyrildiagne/basnet-http) (requires a CUDA GPU)

- You will need the deployed service URL to configure the local server

- Make sure to configure a different port if you're running BASNet on the same computer as the local service

#### Option 2: Use a community provided endpoint

A public endpoint has been provided by members of the community. This is useful if you don't have your own CUDA GPU or do not want to go through the process of running the servce on your own.

Use this endpoint by launching the local server with `--basnet_service_ip http://u2net-predictor.tenant-compass.global.coreweave.com`

### 3 - Configure and run the local server

- Follow the instructions in [/server](/server) to setup & run the local server.

### 4 - Configure and run the mobile app

- Follow the instructions in [/app](/app) to setup & deploy the mobile app.

## Thanks and Acknowledgements

- [BASNet code](https://github.com/NathanUA/BASNet) for '[*BASNet: Boundary-Aware Salient Object Detection*](http://openaccess.thecvf.com/content_CVPR_2019/html/Qin_BASNet_Boundary-Aware_Salient_Object_Detection_CVPR_2019_paper.html) [code](https://github.com/NathanUA/BASNet)', [Xuebin Qin](https://webdocs.cs.ualberta.ca/~xuebin/), [Zichen Zhang](https://webdocs.cs.ualberta.ca/~zichen2/), [Chenyang Huang](https://chenyangh.com/), [Chao Gao](https://cgao3.github.io/), [Masood Dehghan](https://sites.google.com/view/masoodd) and [Martin Jagersand](https://webdocs.cs.ualberta.ca/~jag/)
- RunwayML for the [Photoshop paste code](https://github.com/runwayml/RunwayML-for-Photoshop/blob/master/host/index.jsx)
- [CoreWeave](https://www.coreweave.com) for hosting the public U^2Net model endpoint on Tesla V100s
