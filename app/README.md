# 移动端app搭建步骤

这是一个基于 [Expo](expo.io) / [React Native](#) 的移动应用.
你需要知道怎样用 [expo website](https://expo.io/learn) 预览你的app.

## 配置
1.手机下载Expo(用于运行)，学会如何使用Expo
<br/>
```bash
npm install
```
</br>
修改components/Server.tsx 的代码，IP地址修改成你本地服务器的ip地址:
```js
3: const URL = "http://192.168.0.176:8080"; //写你的ip的地址
```
<br/>

## 运行

```bash
npm start
```
![appNpmStrat](https://github.com/122537067/ar-cutpaste/blob/master/readmeImg/appStart.png)
<br/><br/><br/><br/>
___
以下原文
___
# AR Cut Paste Mobile App

An [Expo](expo.io) / [React Native](#) mobile application.
Please follow instructions from the [expo website](https://expo.io/learn) to see how to preview the app on your phone using the Expo app.

## Setup

```bash
npm install
```

Then update the IP address in `components/Server.tsx` to point to the IP address of the computer running the local server:
```js
3: const URL = "http://192.168.1.29:8080";
```

## Run

```bash
npm start
```
