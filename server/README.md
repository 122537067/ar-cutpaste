# 本地服务器端

## 配置

```console
virtualenv -p python3.7 venv
source venv/bin/activate
pip install -r requirements.txt
```
<br>
注意：如果同时存在python2和python3

```console
virtualenv -p python3.7 venv
source venv/bin/activate
pip3 install -r requirements.txt
```
否则可能会读取不了flask包

## 运行
首先运行[BASNet-HTTP wrapper](https://github.com/122537067/basnet-http) 用作处理图层（放置在deocker）
<br/>
photoshop密码(123456)记得一致

运行python文件：<br/>
```console
python src/main.py \
    --basnet_service_ip="http://X.X.X.X" \
    --basnet_service_host="basnet-http.default.example.com" \
    --photoshop_password 123456
```
<br/>
我的运行方式:
<br/>

```console
python3 src/main.py \
    --basnet_service_ip="http://192.168.0.176" \
    --photoshop_password 123456
```

[image]

<br/><br/><br/><br/>
___
以下原文
___
# AR Cut Paste local server

## Setup

```console
virtualenv -p python3.7 venv
source venv/bin/activate
pip install -r requirements.txt
```

## Run

The `BASNET_SERVICE_HOST` is optional (only needed if you've deployed the service
on a platform using an ingress gateway such as Knative / Cloud Run).

Replace `123456` by your Photoshop remote connection password.

```console
python src/main.py \
    --basnet_service_ip="http://X.X.X.X" \
    --basnet_service_host="basnet-http.default.example.com" \
    --photoshop_password 123456
```
