---
description: 最细粒度的原始数据的完整性、准确性会直接影响到后续的数据分析和应用，因此使用前必须重视在接入环节的数据验证工作
---

# 数据验证

## 总体数据概览

通过SDK/API/文件等方式向方舟上报数据时会经过接收、校验、入库等多个环节，只有入库成功的数据会参与到分析计算当中。

![](<../../../.gitbook/assets/image (515).png>)

**在数据接收环节，当上报数据中 AppKey 与当前项目 AppKey 不匹配时，数据将直接直接被丢弃**

其他 Appkey 符合当前项目时，数据会被分为三类：

**Debug日志**

开启了调试模式（集成SDK时设置 debug =1 或 2 ）时上报的数据将进入Debug 日志，用作测试环节的数据正确性和完整性校验，其中

* debug = 1 的数据仅用于调试，不会入库参与计算
* debug = 2 的数据既可用于调试，又会入库参与计算

**入库成功数据**

开启数据入库模式（集成 SDK 时设置debug = 0 或 2 ）时上报的数据，将进行多重校验，通过校验的数据，将会成功入库，即可用于后续分析和应用；

**入库失败数据**

入库模式下，未通过校验的数据，将进入错误日志，不会参与计算，开发者也可以据此修正上报的数据。

## **Debug 日志**

开发工程师埋点后希望快速了解埋点是否正确，可以设置`Debug = 1 或 2 `开启调试模式，SDK 会向浏览器的控制台中输出日志。日志中会包含一些告警、错误，也会包含上报事件的内容。

以 Chrome 为例，步骤如下：

* 启动 Chrome，并访问已经埋好点的网站
* 按 F12 或 Ctl/Cmd + Alt/Opt + I 打开 “开发者工具”
* 点击 “Console” 页签进入控制台
* 正常浏览页面，接可以看到控制台有大量的日志

![](<../../../.gitbook/assets/image (521).png>)

除了通过客户端验证外，可以用方舟内置的**  Debug 日志 **模块来逐条验证，展示最新 1000 条数据，可选择日期、数据源等进一步过滤。

![](<../../../.gitbook/assets/image (520).png>)

{% hint style="info" %}
从左上角支持切换 **事件日志** 和 **用户日志** 分别查看
{% endhint %}

### 1. 条件过滤

![](<../../../.gitbook/assets/image (522).png>)

#### A. 时间过滤

当一段时间里上报的数据量过大时，可以指定到某个小时或分钟区间来查看

![](<../../../.gitbook/assets/image (523).png>)

{% hint style="danger" %}
日期过滤是基于展示的最新的1000条日志过滤的，也就是说如果今天日志已经超过1000条，则即使昨天实际有测试日志，日期切换到昨天也查询不到结果。
{% endhint %}

#### B. 数据源过滤

一个项目当中会接入多个平台，比如一个应用的Android端、iOS端、网页端等，不同端通常是不同的工程师负责集成SDK，如果只想验证自己集成的数据正确性，则可以选择数据源快速过滤

![](<../../../.gitbook/assets/image (524).png>)



#### C. 其他条件过滤

当要验证某个事件的属性时，可以输入事件ID 来过滤；

当有多个测试设备时，可以输入当前设备绑定的用户ID来过滤，更方便查看；

![](<../../../.gitbook/assets/image (525).png>)

### 2. 实时更新最新数据

当停留在当前页面时，有新的事件产生会实时记录提醒，点击可以加载最新事件；

也可以开始实时刷新按钮，实时加载数据；当实时会产生大量数据时，建议关闭，手动加载最新数据，否则自动加载过快，无法准确验证。

![](<../../../.gitbook/assets/image (526).png>)

### 3. Debug 日志中的错误日志

Debug日志会进行基础的格式、数据类型等校验，当校验不通过时，会直接在列表当中红色标识

![](<../../../.gitbook/assets/image (528).png>)

也可以打开 **仅查看错误日志**开关 查看错误日志

![](<../../../.gitbook/assets/image (527).png>)

### 4. 设置在列表中展示的列

支持自定义展示的列，比如选择展示出常用的设备品牌、型号、IP等方便快速查看

![](<../../../.gitbook/assets/image (254).png>)

### 5. 展开单条事件的属性和JSON数据

点击单条事件，可以展开查看事件属性和JSON数据

![](<../../../.gitbook/assets/image (255).png>)

## **入库成功数据（用于计算）**

展示开启数据入库模式（集成 SDK 时设置debug = 0 或 2 ）时上报的行为数据（Event）（即用于分析计算的数据），最多展示选定时间和条件下的1000条。（注：用户日志用于更新用户属性，不提供单独查询)

![](<../../../.gitbook/assets/image (529).png>)

{% hint style="info" %}
和Debug日志的差异

1. 可以展示选定条件（时间、数据源、事件ID等）下的1000条
2. 需手动点击刷新按钮更新最新数据
3. 不单独展示用户日志
{% endhint %}

## **入库失败数据（错误日志）**

展示关闭调试模式下（Debug=0）和调试模式下（Debug=2）入库失败的数据。通常这也是部分指标在查询时偏差的原因，所以发现错误时，请及时纠正，避免更大的影响。

同 Debug数据验证 的功能相似，同样

* 支持按照事件ID、用户ID、时间来搜索
* 支持筛选可展示的列
* 支持数据的实时更新

除此之外，可以筛选某些特定错误类型下的数据；点击行时，可以展示错误的原因

![](<../../../.gitbook/assets/image (530).png>)



### 错误类型说明

| 错误类型             | 正常情况示例                                                                                   | 错误情况示例                     | 建议解决办法                              |
| ---------------- | ---------------------------------------------------------------------------------------- | -------------------------- | ----------------------------------- |
| JSON 格式异常        | JSON Array对象或 JSON 格式                                                                    | -                          | 上传正确JSON 格式数据                       |
| 标准格式字段校验异常       | -                                                                                        | -                          | 上传正确标准格式字段                          |
| appkey 校验异常      | -                                                                                        | 数据中 appkey 与启动程序中appkey 不同 | 上传一致appkey                          |
| 事件ID不符合校验规则      | Java 命名规范：首位为字母或者$，后面为大小写字母、数字、下划线和$，最大长度125字符                                           | -                          | 上传正确事件ID                            |
| 属性ID不符合校验规则      | Java命名规范：首位为字母或者$，后面为大小写字母、数字、下划线和$，最大长度125字符                                            | -                          | 上传正确属性ID                            |
| 属性值个数超过规定范围      | 上限为300个（包含回数的预置属性和自定义属性）                                                                 | -                          | 减少属性值个数到300个以下                      |
| 属性值不符合规范         | 请查看文档【[Part II-数据接入准备-数据格式](https://docs.analysys.cn/ark/integration/prepare/data-type)】 | -                          | 上传正确属性值                             |
| 属性值上传和现有数值类型不一致  | String                                                                                   | Boolean                    | 上传一致类型的属性值                          |
| 属性值类型不支持         | 类型仅包含：String/Number/Boolean/数组                                                           | -                          | 上传支持的属性值类型                          |
| 显示用户登录，但是数据库中不存在 | -                                                                                        | -                          | 确定该用户是否绑定                           |
| IP解析异常           | -                                                                                        | -                          | 联系运维                                |
| 数据信息超过限定时间       | -                                                                                        | -                          | 请重新确认数据接收时间范围（以当前时间为准，前10天内和未来3小时内） |
| 程序异常             | -                                                                                        | -                          | 联系易观运维                              |

{% hint style="info" %}
以上内容没有解答我的问题？[点击我进入方舟论坛去反馈](https://www.analysysdata.com/forum/index) 🚀
{% endhint %}
