# 说明文档

项目无Wiki，此说明文档包含了项目所有相关内容。包括项目介绍、使用说明等。

## 前言

一切有为法，如梦幻泡影；如露亦如电，应作如是观。

### 缘起

　　我自己多年来一直使用通达信公式选股。近期越发感觉到通达信公式的局限性（大智慧同花顺公式和通达信都有同样局限性），比如变量无法二次赋值、没有循环、IF语句简陋，且软件自带公式评测功能鸡肋。更重要的是**通达信公式都是基于短周期的判断**，比如不管是MACD金叉、cross上穿还是创历史新高，皆为“当前周期日”的结果，无法判断类似“此为上涨第几浪，每个浪的高低价各是多少”。而如果用周线周期选股，那只有每周五收盘以后才可以选，会错失先机。月线更是不可能用到。

　　因此，我有了两个核心需求：盘中选股以及策略回测。这又延伸出了数据采集、数据加工、行情监视等需求。另外为了隐私考虑，所有第三方导入库、借鉴的代码都需开源，本地化，不云端。

### 什么是量化

　　我的理解，“量化”一词有两层释义。狭义上是指把思路变为计算机代码，包括通达信公式、python代码等；广义上是指在狭义释义的基础上，通过计算机自动完成整个选股和交易的过程。

### 为什么量化

　　然而量化又是投资过程中必须要完成的阶段。你有了一个选股思路，不管是长线投资的还是短线投机、不论是看基本面还是看技术面，总之你想把思路转化为选股策略，把思想转变为选股公式，这一过程本身就是量化。再之后，为了确定策略是否有效、收益率如何，又必然需要做策略回测来验证。最后，为了防止人性对交易过程的干扰，可以考虑使用自动化交易。

### 量化的优点

1. 选股。当把选股思路量化为代码后，计算机可以快速准确的帮你选出你想要的股票。
2. 下单速度。触发买入、卖出条件后，计算机可以在毫秒级别内完成下单操作。人为操作需要“打开交易软件-填股票代码-填金额-填数量-点下单”。这还没有考虑下单前，人们会来回犹豫所浪费的时间。

### 量化了就能赚钱？

　　python、量化过程、量化平台都只是工具，核心是交易策略，是交易思想。交易的目的是赚钱，不是学编程当程序员，也不是沉迷于玩数据中不可自拔，代码写的再高级精炼，不赚钱统统白搭。现在网上很多收费课程、量化平台，都是“卖铲子”的，核心的可以能稳定赚钱的量化策略，绝无一家提供。

　　就我个人而言，我不赞同完全把重心放在全自动量化交易上，而忽视基本面和技术面。对于短线来说，不确定性太多。比如，1分钟K线几乎处于“混沌”状态，根本没有逻辑和趋势可言。而周期越大的K线，越能体现出趋势和力度，突然反转的可能性越小。对于长线来说……还未听说过有把程序化交易用于长线的事例。

> 交易这门手艺发展了这么多年，流派可谓五花八门，有看基本面搞价值投资的，有看K线搞技术指标的，有学江恩，缠论数波浪画中枢的，有分析资金面的，分析市场情绪的，有结合原始数据做日内波段的，有恨不得把服务器架在交易所对面做高频的，有搞一箱子GPU做automl，深度学习和强化学习的，有搞对冲的，搞多因子的，搞指数增强的，有搞MOM组合管理的，有搞一堆艰深晦涩的微分方程做衍生品套利的，当然，也有靠求神拜佛和拍脑门跺地板的。每种流派都有一些人奉为圭臬，还有一批人弃如敝履，而且时不时的还会冒出几个新的流派出来，令人眼花缭乱，有些摸不到头脑。
>
> 不知道哪个著名的人曾说过，如果你没有自己的思想，那你的脑子注定会成为其他人思想的跑马场。上面的这一堆思想和流派，既然能够出现并且流传下来，还能够有一批拥趸和死忠，也就表明它们确实是市场的本质或者圣杯在某个维度的一个映射或投影，但也仅仅只是一个投影而已。学习它们只是为了能够从更多的角度去窥视那个交易的圣杯，进而一点点的深化，完善和验证自己的交易思想和理论体系，最终通过一个承载着自己思想体系的工具来将思想兑换成实际的收益。在这个市面上出现的每一种付费编译的或者免费开源的交易软件都是固定的，即使在不断更新迭代也只是按照开发团队的思路来进行，包括QA在内，不可能有一个软件或者项目能够满足所有可能的交易思想，自然也就无法让你自由的学习，验证，归纳和吸收这些思想中的精华。因此，如果你没有定制化的开发交易工具的能力，而只能使用现有的工具的话，你的思想和自由意志就这样被别人的工具所局限住了。——[对QUANTAXIS的设计理念的思考和一些感悟](http://www.yutiansut.com:3000/topic/5f5ee1775778f910c1ba7a97)

## 项目介绍
- 使用python进行股票历史数据下载和分析选股。除了选股策略以外，其他都可公开。
- git网站上有很多优秀开源量化平台项目。本项目与其他项目的区别是，本项目侧重于选股、回测所需数据的导入工作。有了历史数据和选股策略，选择哪个量化平台做回测都是很轻松的事情了。
- 业余编程水平，需求导向。才疏学浅，刚学python几个月时间。git主要作为云端git库使用。无任何解答服务。
- 力求选择最稳定可靠的数据获取方式。虽然网上有很多数据源平台，但都受制于“积分”、带宽、平台是否更新等，完全是把程序主动权交到了对方手里。因此本项目所有数据依靠本地通达信软件导出提供。感谢通达信，真是个好公司！不止数据容易提取，各种和谐加强版也很好用。

### 项目进度

#### 已完成功能

- 读取本机通达信文件，导出未除权日线数据、股本变迁数据、全A股全年份财务报告数据。
- 财务报告数据自动判断是否需要更新
- 日线数据本地前复权计算处理。日线数据只追加当日数据，加快数据更新速度。
- 非盘中、历史数据选股（选股策略你得自己写）

#### 待完成功能

需求优先级由高到低排序

- 盘中选股
- 回测（是指本项目提供数据和策略，接入本地化的量化回测平台进行回测，预计会使用BackTrader）
- 数据存储方式优化。目前使用csv文件，性能略差。但这个也不是特别需要。
- ~~多线程优化处理。技术太难，我完全不会。~~

### 数据来源

基础数据来源：

|   数据名称   |                数据来源路径                 |                       数据本身更新方式                       |
| :----------: | :-----------------------------------------: | :----------------------------------------------------------: |
|   日线数据   |  解析本机通达信离线数据/vipdoc/sh(sz)/lday  | 完整数据通过通达信软件手动更新，当日数据可在通达信设置自动更新 |
| 财务报告数据 |      解析本机通达信离线数据 /vipdoc/cw      |                       代码自动维护更新                       |
| 股本变迁数据 | 解析本机通达信离线数据 /T0002/hq_cache/gbbq |                运行通达信时，通达信可自动更新                |

其他数据可以由基础数据本机计算得出。比如前复权、流通市值、市盈率等。

## 使用说明

写的简陋。有空了再细化。

### 初次使用

1. 克隆/下载项目zip包，解压缩。项目无需pip安装
2. 查看软件架构章节，自行安装支持库
3. 打开user_config.py，配置好各路径
4. 参照CeLue模板.py，照猫画虎自己写策略，保存为celue.py
5. 接着看数据更新章节

### 数据更新

每天16时，通达信更新当日日线数据。你可手动更新，或在通达信设置-设置1标签，勾选“定时提示下载日线”并设置为16点。在通达信软件运行的情况下，每天16点通达信自动更新当日数据。

通达信更新后，再进行下面的操作：

1. 运行readTDX_cw.py，更新财报和股权变迁数据

2. 运行readTDX_lday.py，输入y完全生成前复权日线数据，其他任意输入只处理需要更新的数据

3. 运行xuangu.py，查看选股结果

### 二次开发

想给日线计算添加自己的数据，在func_TDX.py的make_fq函数，加到下面语句前。

`if len(start_date) == 0 and len(end_date) == 0:`

财报文件所有字段释义，查看“util_docs\专业财务文件字段含义对照表.txt”


## 软件架构
|      软件/库      |   版本   |
| :---------------: | :------: |
|    windows 10     |   20H2   |
| 通达信开心果版本  | v2020.12 |
| python (anaconda) |  3.8.5   |
|       pytdx       |   1.72   |
|      ta-lib       |  0.4.19  |

其他缺什么库运行时报错自己pip安装一下

## 开发日志

[点我打开](https://gitee.com/wkingnet/stock-analysis/wikis/pages?sort_id=3514436&doc_id=1209752)