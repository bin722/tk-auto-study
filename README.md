# 青年大学习/团课自动打卡

![](https://github.com/838239178/tk-auto-study/workflows/auto-study/badge.svg) ![](https://img.shields.io/github/stars/838239178/tk-auto-study) ![](https://img.shields.io/github/forks/838239178/tk-auto-study) ![](https://img.shields.io/badge/Python-3.9-green.svg)

[此处展示最近更新日志，完整日志搓这里](./doc/Log.md)

> **2022.03.06**: :warning: **[重要更新]** 新学期新气象，GithubAction已经可用使用了！！新增Bark消息推送模式（beta) 
>
> 2022.03.11: 经用户反馈，去除了OCR功能模块，现在不需要申请OCR账号，添加了更多代理源 改善代理异常的处理 提高可用性
>
> 2022.03.26: 感谢 @miscdec 对开源库的贡献，现在添加了push_plus推送渠道，并修复了一些异常。
>
> 2022.03.27: 代理池极不稳定
>
> 2022.03.30: 感谢 @Dark-Existed 贡献了Docker部署脚本，请使用环境变量配置相关参数

🤺妈妈再也不用担心我团课没看被团支书赶着催了

### 点个:star:再走吧,❤感谢大家的Star和Fork,有问题可以发issue

**仅供福建共青团团员学习交流使用** 

~~浙江团员可以点击这里[青春浙江](https://gist.github.com/838239178/ddad90e8c5e52f5fa8f0febea6109f24)~~

### 参与贡献！

:pen: 如果你有新的或更好消息推送方式 请参考 [消息推送贡献文档](./doc/send_module_rule.md) 做出你的贡献！

## 使用方法

#### 🍎pub_key:

```
A7E74D2B6282AEB1C5EA3C28D25660A7
```

#### 部署在平台上定时执行

可以是服务器，本地，和GitHubActions，这里只介绍如何在GitHubActions中运行，其他运行方式请参考main.py中的注释

- fork该项目到你的库中
- 添加三个secrets，分别为：username,  pwd,  pub_key

- 将[该文件](./.github/workflows/run.yml)中的`#`删除并修改cron为你想要触发的时间，默认是每周三14点运行一次，cron如何写请自行百度
 
  ![image](https://user-images.githubusercontent.com/55338151/161259594-21812419-25e3-4b1f-b64f-e06b826351b8.png)

- 进入 Actions 中手动触发一次（点击auto-study 右边 Run workflow)，测试是否成功
  
  ![image](https://user-images.githubusercontent.com/55338151/161258385-eccd7f2f-8b7e-4002-aa8b-c436e96c01d7.png)

> `1.2.8` 版本以上可以使用Docker脚本运行，使用环境变量配置参数（格式同Actions)，可能无法配置多人打卡，可以尝试使用`\n`换行符（未测试）

### 如何在服务器上部署

#### crontab

克隆项目并更改配置文件名称

```shell
git clone https://github.com/838239178/tk-auto-study.git && \
cd tk-auto-study && \
mv config.json.bak config.json
```

按照要求填写配置文件

```shell
vi config.json
```

修改 crontab

```shell
crontab -e
# 将下面这行复制到里面，cd的路径按照需要更改
00 08 * * 3 cd /root/tk-auto-study && python3 main.py >> crontab.log 2>&1
# 或者
00 08 * * python3 /root/tk-auto-study/main.py >> crontab.log 2>&1
```

使用 `crontab -l` 查看是否修改成功

#### docker

除了crontab也可以使用目录下的`docker-compose.yml`，不需要填写 `config.json` 但需要修改文件内的`environments`

```shell
docker-compose up -d
```

## 可选消息推送

> 仅 `1.2.2` 版本及以上可用

使用消息推送 如微信推送、QQ推送

### 配置

GithubAction用户可通过添加secrets：send_type, send_key, send_mode 来使用消息推送

普通用户可查看最新的 `config.json.bak` 浏览新配置项

**配置项解读**

| 配置项    | 说明                                                         | 可选值                                        |
| --------- | ------------------------------------------------------------ | --------------------------------------------- |
| send_type | 消息推送类型 **不填写则不推送**                              | [server_chan](./doc/send_help/server_chan.md) [bark(Beta)](./doc/send_help/bark.md) [push_plus](./doc/send_help/push_plus.md) |
| send_key  | 消息推送服务的密钥 在推送服务的官网注册获得                  |                                               |
| send_mode | 推送模式 打卡失败时推送(fail) 打卡成功时推送(success) 无论成功与否都推送(both) **默认失败时推送** | fail success both                             |

## 多人打卡

> 仅支持 `1.2.3` 以上版本

配置多个账号一起打卡

1. 在 `Github Action` 上配置

    添加新secrets `EXT_USERS`, 按以下格式填写账号：
    
    ```text
   手机号1 密码1
   手机号2 密码2
   ```
   
   原先配置的secrets不需要改动，建议自己保存好多人的账号密码，以便以后增加或删除账号

2. 在本地 `config.json` 上配置

   参考 [config.json.bak](./config.json.bak) 的内容添加新的配置，原配置不需要改动

## Stargazers over time

[![Stargazers over time](https://starchart.cc/838239178/tk-auto-study.svg)](https://starchart.cc/838239178/tk-auto-study)

## 赏我一杯Coffee

![qq_pic_merged_1633171137809](https://cdn.jsdelivr.net/gh/838239178/PicgoBed/img/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f3833383233393137382f506963676f4265642f696d672f313633333137313136342e6a7067.jpg)![qq_pic_merged_1633171137809](https://cdn.jsdelivr.net/gh/838239178/PicgoBed/img/qq_pic_merged_1633171137809.jpg)

