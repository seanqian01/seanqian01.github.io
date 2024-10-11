---
layout:       post
title:        "怎样将TradingView的提醒信号接入到自己的系统内"
author:       "Seanqian"
header-style: text
catalog:      true
tags:
    - tradingview 
    - tradingview alert
    - tradingview报警
    

---

##### Tradingview网站上面报警提醒的设置
先要在Tradingview里设置对应的webhook信号提醒的方式.

![webhook2_20240402173201542387.png](https://s2.loli.net/2024/10/11/tGElTbHNiJvZS7e.png)
	1.确定标的,具体是做哪个期货合约
	2.确定K线周期,具体报警也要跟着周期来走.每个不同的周期,报警的警示信息webhook就需要另外设置
	3.确定产生报警的信号策略(指标),在tradingview里面一大把指标,在指标的基础上产生对应的信号.
	4.确定webhook送出的信号内容.(通常是用json的方式将信息送到对应的接口处)


 示例信号的json代码如下:
   {
    "secretkey": "itsthesecretheyhey",
    "symbol":"{{ticker}}",
    "scode":"RBK2405",
    "contractType": "1",
    "price": "{{close}}",
    "action": "open long",
    "alert_title": "RBK2405_螺纹钢合约信号_开仓做多",
    "time_circle":"1m"
  }

- 通常信号里面的数据跟自己在django框架的api接收的接口要有对应关系.这些字段需要提前在django框架里新增
  然后根据接口的定义,比如contracttype=1是啥意思,自己在数据库里面定义好,接口就可以直接调用了.
  
  按照我现在设置webhook的报警的经验,通常期货的报警通知信号,一个周期一个标的要搞四个报警信号:
  分别是开多仓,平多仓,开空仓,平空仓.
  以前放的是简单的sell和buy发现不够用,建议分成四个,这样在处理信号的类型的时候可以对号入座,对于后期的仓位管理也是有好处的.
  
  通过这个webhook放api接口进入到django框架内,django后台的信号的呈现是下图这样的:

![webhook3_20240402174138809033.png](https://s2.loli.net/2024/10/11/CLO6XtoBkMPdVlF.png)

先把报警信号收进来,接口的写法这里就不赘述了,
值得一提的是接口的代码里,本来想加入队列,让接口可以在队列里不断的接收tradinview的报警.
后面实践下来发现只有高频可能才需要有队列,正常的1分钟以上的K线周期,信号接收基本上不用队列就可以正常正确的接收下来了.

后面得空了讲一下信号过滤的简单规则.
