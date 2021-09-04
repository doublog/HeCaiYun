# HeCaiYun

和彩云自动打卡签到

搬运自[xuthus5/HeCaiYun](https://github.com/xuthus5/HeCaiYun)，改为github action版本

需要自行在`.github/workflows/main.yml`添加定时任务

## 服务器运行

安装脚本所需依赖
```
pip3 install request
```

### 获取Cookie

打开[和彩云签到有礼 (10086.cn)](https://caiyun.feixin.10086.cn:7071/portal/newsignin/index.jsp)页面=>登录=>按`F12`打开开发者工具-Network=>F5刷新页面=>过滤参数填`caiYunSignIn`=>找到`caiYunSignIn.action`请求=>点击查看**cookie**，只要从`JSESSIONID`到第一个`;`，即类似于`JSESSIONID=8BCB8BCB8BCB8BCB8BCB8BCB8BCB8BCB-n1;`的内容。

修改脚本代码13-16行参数
```
OpenLuckDraw = True if os.getenv("LUCK_DRAW") == 'true' else False  # 是否开启自动幸运抽奖(首次免费, 第二次5积分/次) 不建议开启 否则会导致多次执行时消耗积分
PUSHPLUS_TOKEN = os.environ['PUSHPLUS_TOKEN']  # PushPlus Token
Cookie = os.environ['COOKIE']  # 抓包Cookie
Referer = os.environ['REFERER']  # 抓包referer
```

## Secret

**`Settings`->`Secrets`->`New repository secret`，添加以下Secret：**
- `COOKIE`：抓包Cookie
- `REFERER`：抓包referer
- `PUSHPLUS_TOKEN`：PushPlus Token
- `LUCK_DRAW`：是否开启自动幸运抽奖. `true`:开启; 不填/其他:不开启. (首次免费, 第二次5积分/次) 不建议开启 否则会导致多次执行时消耗积分
