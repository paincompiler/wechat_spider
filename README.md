
# wechat_spider 微信爬虫

*This project is a fork of [lqqyt2423/wechat_spider](https://github.com/lqqyt2423/wechat_spider). Please contact the original author for the license info.*

基于Node 的微信爬虫，通过中间人代理的原理，批量获取微信文章数据，包括阅读量、点赞量和评论等数据。使用代理模块 Anyproxy。

## Getting Started

### 安装前

- Node 版本大于v8.8.1
- MongoDB 版本大于v3.4.6

### Installation

```shell
git clone https://github.com/lqqyt2423/wechat_spider.git
cd wechat_spider
npm install
```

本项目基于代理模块Anyproxy，解析微信HTTPS 请求需在电脑和手机上都安装证书。可参考：[Anyproxy 文档](https://github.com/alibaba/anyproxy)。

## Usage

```shell
cd wechat_spider
npm start
```

1. 确保电脑和手机连接同一WIFI ，`npm start` 之后，命令行输出`Http proxy started at xx.xx.xx.xx:8101` 类似语句，手机设置代理为此IP 和端口
2. 手机上测试打开任一公众号历史文章详情页和文章页，观察电脑命令行的输出，查看数据是否保存至MongoDB
3. 自动翻页抓取数据需配置`config.js`

### 可视化界面

```shell
cd client && npm install && npm start
```

第一次进入`client` 运行`npm install` 之后，以后可直接在项目根目录运行`npm run client` ，根据命令行的输出地址，在浏览器中打开此网址即可。

### 从MongoDB 导出数据

```shell
mongoexport --db wechat_spider --collection posts --type=csv --fields title,link,publishAt,readNum,likeNum,msgBiz,msgMid,msgIdx,sourceUrl,cover,digest,isFail --out ~/Desktop/posts.csv
```

以上命令会导出数据至桌面的`posts.csv` 中。具体的个性化导出请参考MongoDB 文档或者自己编写。
