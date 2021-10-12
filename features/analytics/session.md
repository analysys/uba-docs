# Session 分析

{% hint style="info" %}
**session分析功能的使用需要相应平台集成支持该功能的SDK：**

Android SDK ：v4.1.2 及以上\
iOS SDK： v4.1.2 及以上\
JS SDK：v4.1.3 及以上\
小程序 SDK：v4.1.3 及以上
{% endhint %}

{% hint style="info" %}
**session分析功能支持自定义切割规则：**

v4.4.0 及以上
{% endhint %}

除了分析每一个事件之外，方舟还支持基于 Session 的分析。

Session，即会话，是指在指定的时间段内在您的网站/H5/小程序/APP上发生的一系列用户行为的集合。例如，一次会话可以包含多个页面浏览、交互事件等。Session 是具备时间属性的，根据不同的切割规则，可以生成不同长度的 Session，关于方舟的 Session 的默认规则为“系统预置规则”，具体请参考：[Session 规则](channel/session.md)。其他自定义切割规则可以在管理-元事件管理-[Session管理](https://docs.analysys.cn/ark/features/project-manegement/yuan-shu-ju-guan-li/session)中创建新的session切割规则或修改原有session切割规则。

![](<../../.gitbook/assets/image (155).png>)



在 Session 分析中，易观方舟支持多种度量 Session 访问质量的指标，包括：

* 访问次数
* 人均访问次数
* 总访问时长
* 单次访问时长
* 单次访问深度
* 跳出次数
* 跳出率
* 退出次数
* 退出率
* 人均访问时长
* 总页面停留时长
* 平均页面停留时长

{% hint style="info" %}
跳出次数和跳出率仅支持 Web/H5/小程序的统计分析
{% endhint %}

同时，不同于事件分析，Session 分析中额外支持了一些维度的细分，以满足特定场景下针对 Session 分析的需求，包括：

* 渠道来源分组：用以区分每次访问的渠道来源，仅适用于 Web/H5/小程序
* 浏览页面数：以步长5为间隔，统计每次浏览页面数的分布情况
* 着陆页：用以区分每次访问的着陆页，可以评价不同着陆页的访问质量
* 退出页：用以区分每次访问的退出页，可以评价不同页面的退出情况，找到退出率高的页面进行优化
* 访问时长：按照 0-3 secs，3-10 secs，10-30 secs，30-60 secs，1-3 mins，3-10 mins，10-30 mins，30-60 mins，1 hour 以上的区间进行划分，统计每次访问的时长分布

{% hint style="info" %}
根据实际分析场景，一些指标和维度之间不能形成细分关系，比如：着陆页和退出次数、退出率；退出页和跳出次数、跳出率等，相关逻辑关系已经体现在产品交互中，用户选择相应的 Session 指标，在细分维度中都是具备实际分析意义的可选维度
{% endhint %}

## 功能说明

![分析-Session 分析](<../../.gitbook/assets/image (5).png>)

同事件分析类似，Session 分析支持多指标、多维度和多过滤条件，同时也支持多用户分群之间的横向对比，在分析展现层面，支持以下图表类型：

* 趋势图
* 面积图
* 时间维度柱图
* 柱形图
* 饼图
* 数值图
* 表格

同时，在 Session 分析中，支持按照日、周、月三种不同粒度来进行统计分析，用户可以根据查询数据的时间跨度来选择合适的粒度进行分析。



{% hint style="info" %}
以上内容没有解答我的问题？[点击我来反馈](https://support.qq.com/products/118522/) 🚀
{% endhint %}
