# 自定义监控

{% hint style="info" %}
自定义监控告警功能的使用需要相应方舟版本：

v4.1.2 及以上
{% endhint %}

在相对稳定的产品中，运营、市场和产品相关人员都会有持续关注的一些关键数据指标，当这些数据指标波动较大，发生异常数据时，需要及时提醒。

因此，方舟推出了“自定义监控”功能，可以对关键、核心的数据指标进行7\*24小时实时监控，当满足预先设置好的阈值后，通过邮件或告警信息等不同响应级别方式第一时间发送通知。

## 1 创建监控告警

![](https://imguserradar.analysys.cn/fangzhou/img/2019/01/201901251157108113.gif)

### **1.1 设置基本信息**

* 监控名称：填写监控告警名称（不超过50个字符）
* 监控指标：选择你要监控的指标及条件，该指标类型与事件分析中的指标相同。例如选择监控的某一事件触发的用户数以及转化事件等。 

![ ](https://imguserradar.analysys.cn/fangzhou/img/2019/01/201901251723574082.png)

### **1.2 设置告警条件**

* 选择期望计算时间：包含每小时、每天、每周一、每月第一天，以及相应计算计算具体时间（精确到10分钟级别），具体可选范围以及相应计算周期如下：

| 计算时间   | 可选小时分钟 | 计算粒度 |
| ------ | ------ | ---- |
| 每小时    | 分钟     | 小时   |
| 每天     | 小时:分钟  | 天    |
| 每周一    | 小时:分钟  | 周    |
| 每月第一天一 | 小时:分钟  | 月    |

![ ](https://imguserradar.analysys.cn/fangzhou/img/2019/01/201901251916268887.png)

* 选择对比方式：

| 比较方式 | 和谁比   | 可以比什么 |
| ---- | ----- | ----- |
| 大于   | 特定值   | 数值    |
| 小于   | 特定值   | 数值    |
| 增加超过 | 对比周期值 | 数值    |
| 增加超过 | 对比周期值 | 百分比   |
| 减少超过 | 对比周期值 | 数值    |
| 减少超过 | 对比周期值 | 百分比   |

同时针对不同的计算时间粒度，可选择不同的对比周期值

| 计算周期 | 特定值 | 前一小时 | 前一天同一小时 | 前一天 | 上一周同一天 | 上一月同一天 | 上一年同一天 | 上一周 | 上一月同一周 | 上一年同一周 | 上一月 | 上一季同一月 | 上一年同一月 |
| ---- | --- | ---- | ------- | --- | ------ | ------ | ------ | --- | ------ | ------ | --- | ------ | ------ |
| 小时   | √   | √    | √       |     |        |        |        |     |        |        |     |        |        |
| 天    | √   |      |         | √   | √      | √      | √      |     |        |        |     |        |        |
| 周    | √   |      |         |     |        |        |        | √   | √      | √      |     |        |        |
| 月    | √   |      |         |     |        |        |        |     |        |        | √   | √      | √      |

示例：下图的选择就是让监控告警“每天07:00:00的时候计算所选指标 本期值（前一天的数据）和对比值（大前天的数据），如果本期值-对比值＞100 时就触发告警信息或告警邮件”

![ ](https://imguserradar.analysys.cn/fangzhou/img/2019/01/201901252003380222.png)

### **1.3 设置告警方式**

默认为触发告警消息，也可以针对需要及时响应的监控告警添加邮件告警方式 

![ ](https://imguserradar.analysys.cn/fangzhou/img/2019/01/201901252014290304.png)

## 2 查询告警消息

通过点击触发的告警消息的【查看详情】按钮，可以进入事件分析，在图表中查看具体异常点，并通过细分维度等方式快速找到异常原因，从而采取有效改进措施。 

![ ](https://imguserradar.analysys.cn/fangzhou/img/2019/01/201901251157357360.gif)

## 3 自定义监控管理

在自定义监控告警列表中可以查看、修改、复制、删除创建过的监控。 

![ ](https://imguserradar.analysys.cn/fangzhou/img/2019/01/201901252054282807.png)

## 4 特别说明

* 权限：仅有管理员可以创建、修改、删除监控告警，其他成员仅可以查看。
* 特别情况：如果设置对比方式为百分比，而对比值为0，则不会触发告警，因为该种情况计算结果为无穷大。
* 发送邮件：如果私有化部署客户，没有配置邮箱设置，需先完成配置。



{% hint style="info" %}
以上内容没有解答我的问题？[点击我来反馈](https://support.qq.com/products/118522/) 🚀
{% endhint %}
