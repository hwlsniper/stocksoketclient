# 大师兄股票实时行情客户端

客户端采用JAVA语言开发，支持Linux|Windows多平台运行，主要用来分发股市Level1实时行情。大师兄实时行情工具集成了股市实时行情，五档，财务数据以及板块涨跌幅榜，个股涨跌幅榜，日K、周K、月K、1分钟、5分钟、15分钟、30分钟、60分钟K线历史数据于一体，采用Redis缓存数据库进行存储，快速便捷。数据使用也非常方便，不用复杂的计算，基本都是拿来就用，任何人都无须股市知识的情况下灵活使用。现在推出公测版，因为服务器资源有限，视情况切断试用通道，理解万岁！！！

目前只支持A股行情，实时行情延时3秒左右

 
 
## 接口DEMO：

1、实时行情接口：http://kline.api.shqingsi.cn/v1/quotes.php?code=sh000001,sh600000

返回字段：

lastTime：最新时间

lastDate：最新日期

code：股票代码

name：股票名称

volumnPrice：成交额 单位元

volumn：成交量

circulationValue：流通市值

totalValue：总市值

type：0=个股 1=指数

isStop：是否停牌 1=停牌

peRatio：市盈率

swing：振幅

turnoverRate：换手率

cityNetRate：市净率

price：当前价格

openPrice：开盘价

highPrice：最高价

lowPrice：最低价

closePrice：收盘价

sell_5：卖五价格

sell_4：卖四价格

sell_3：卖三价格

sell_2：卖二价格

sell_1：卖一价格

sell_5_s：卖五数量

sell_4_s：卖四数量

sell_3_s：卖三数量

sell_2_s：卖二数量

sell_1_s：卖一数量

buy_5：买五价格

buy_4：买四价格

buy_3：买三价格

buy_2：买二价格

buy_1：买一价格

buy_5_s：买五数量

buy_4_s：买四数量

buy_3_s：买三数量

buy_2_s：买二数量

buy_1_s：买一数量





2、分时图接口：http://kline.api.shqingsi.cn/v1/kline.php?code=sh000001&cycle=timeline&fq=data

返回数组：

数组格式为：[日期，时间，价格，成交量，成交额]


3、K线图接口：

  日线（不复权）：http://kline.api.shqingsi.cn/v1/kline.php?code=sh000001&cycle=day&fq=data

  返回数组：

  数组格式为：[日期，开盘价，最高价，最低价，收盘价，成交量，成交额]

  
  日线（前复权）：http://kline.api.shqingsi.cn/v1/kline.php?code=sh000001&cycle=day&fq=before

  返回数组：

  数组格式为：[日期，开盘价，最高价，最低价，收盘价，成交量，成交额]

  
  日线（后复权）：http://kline.api.shqingsi.cn/v1/kline.php?code=sh000001&cycle=day&fq=after

  返回数组：

  数组格式为：[日期，开盘价，最高价，最低价，收盘价，成交量，成交额]

  
  周线：http://kline.api.shqingsi.cn/v1/kline.php?code=sh000001&cycle=week&fq=data

  返回数组：

  数组格式为：[日期，开盘价，最高价，最低价，收盘价，成交量，成交额]

  
  月线：http://kline.api.shqingsi.cn/v1/kline.php?code=sh000001&cycle=month&fq=data

  返回数组：

  数组格式为：[日期，开盘价，最高价，最低价，收盘价，成交量，成交额]

  
4、搜索股票：http://kline.api.shqingsi.cn/v1/search.php?key=0001

  返回数组：

  数组格式为：[股票代码，拼音首字母，股票名称，类型]


5、行业概念地区涨幅榜：
   行业涨幅榜：http://kline.api.shqingsi.cn/v1/plateranking.php?typeCode=hangye

   地区涨幅榜：http://kline.api.shqingsi.cn/v1/plateranking.php?typeCode=diyu

   概念涨幅榜：http://kline.api.shqingsi.cn/v1/plateranking.php?typeCode=gainian

   返回字段：

code:股票代码

name：股票名称

change：股票涨跌额

changeRate：股票涨跌幅

id:行业ID编号

title：行业名称

rate：行业涨幅



6、行业个股涨幅榜：http://kline.api.shqingsi.cn/v1/updownlist.php

返回字段：

code:股票代码

name：股票名称

change：股票涨跌额

changeRate：股票涨跌幅

id:行业ID编号

title：行业名称

rate：行业涨幅

 
 基于此行情得移动端DEMO（狙击手APP）下载地址：https://app.download.ebamai.com/sniper/index.php
 

## 环境要求：
JAVA JDK 1.8及以上，JDK下载地址：http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

安装Reids环境 下载地址https://redis.io/

CPU 双核 4G内存及以上
 

## 配置config.properties：

#本地redis

redisServer = 127.0.0.1

redisPort = 6379

redisPassword = 123456

#路由 不可修改

socketServer = http://114.55.140.140:8111/v1/
 
#是否采集K线历史数据

isCollectionHistoryKline = false

#是否采集分钟K线历史数据

isCollectionHistoryMinKline = false

#k线本地保存地址 为空默认为程序运行目录

klineSavePath =


## 运行：

启动：

java -jar /data/stocksocketclient/stocksocketclient.jar 
 
重启： 

java -jar /data/stocksocketclient/stocksocketclient.jar 1 
 
同步所有K线历史数据： 

java -jar /data/stocksocketclient/stocksocketclient.jar 3
 

## 数据使用方式：

#运行初始化后即可在redis找到实时行情数据，具体操作步骤如下：

#获取某个股票实时行情数据：

select 0

get sh000001
 
#返回json字符串：

{"buy_1":0,"buy_2":0,"buy_3":0,"buy_4":0,"buy_5":0,"buy_1_s":530787800,"buy_2_s":0,"buy_3_s":0,"buy_4_s":0,"buy_5_s":0,"code":"sh000001","closePrice":3154.65,"cityNetRate":0,"circulationValue":0,"highPrice":3156.73,"isStop":0,"lastDate":"2018-05-25","lastTime":"15:01:03","lowPrice":3131.07,"name":"\u4e0a\u8bc1\u6307\u6570","openPrice":3148.41,"price":3141.3,"peRatio":0,"swing":0,"sell_1":0,"sell_2":0,"sell_3":0,"sell_4":0,"sell_5":0,"sell_1_s":621543700,"sell_2_s":0,"sell_3_s":0,"sell_4_s":0,"sell_5_s":0,"type":1,"totalValue":0,"turnoverRate":0,"volumn":12861084000,"volumnPrice":166554042368}
 
#获取股票搜索库

select 2

keys *

搜索某个关键词股票

keys *xxx*
 
 
#板块涨幅榜

select 8

#行业涨幅

get Hangye_UpListKey

#概念涨幅

get Gainian_UpListKey

#地域涨幅

get Diqu_UpListKey

#个股涨幅榜

get Stock_UpdownList

#换手率榜

get Stock_UpdownList_turnoverRate

#振幅榜

get Stock_UpdownList_swing

#总市值排行榜

get Stock_UpdownList_totalValue

#流通市值排行

get Stock_UpdownList_circulationValue

#除权数据

hgetall ExRight_Tables

hget ExRight_Tables 600000

返回数据：

[{"code":"600000","datetime":"2000-07-06","give":0.0,"pei":0.0,"peiPrice":0.0,"profile":0.15000000596046448},{"code":"600000","datetime":"2002-08-22","give":0.5,"pei":0.0,"peiPrice":0.0,"profile":0.20000000298023224}]

字段含义：

code:股票代码

datetime：日期

give：每股送

pei：每股配

peiPrice:配股价

profile：每股红利


#财务数据

hgetall Financial_Tables

hget Financial_Tables 600000

返回数据：

{"code":"600000","datetime":"20180830","ZGB":"2935208.00","GJG":"180199.00","LTAG":"2810376.50","ZZC":"6091758592.0","LDZC":"0.0","GDZC":"31543000.0","JZC":"440855008.0","ZYSY":"82256000.0","ZYLY":"0.0","YYLY":"34164000.0","SHLY":"28900000.0","JLY":"28569000.0","DY":" 16","HY":" 1","ZBNB":"6","SSDATE":"19991110"}

字段说明：

code：股票代码

datetime：日期

ZGB:总股本

GJG:国家股

LTAG:流通A股

ZZC:总资产

LDZC：流动资产

GDZC：固定资产

JZC：净资产

ZYSY：营业收入

ZYLY：主营利润

YYLY：营业利润

SHLY：税后利润

JLY：净利润

DY：地域

HY：行业

ZBNB：资料月份 9 代表三季报 12代表年报

SSDATE：上市日期

 

## 下载地址

官方更新地址：

https://github.com/dangfm/stocksoketclient/

接口DEMO：https://github.com/dangfm/KLineApi

移动端DEMO：https://app.download.ebamai.com/sniper/index.php

QQ交流群：大师兄股票实时行情

群   号：789599606



仅供学习研究使用，请勿用于商业用途！
