# 合规相关

如果您的app 有《隐私政策》，弹出《隐私政策》后用户不同意，可能需要停止sdk的数据采集和上报，下次用户同意《隐私政策》后需要恢复采集和上报，可以调用此接口：

```java
AnalysysAgent.setDataCollectEnable(false);
```

您务必告知用户您选择易观方舟SDK服务，请在《隐私政策》中增加如下参考条款：

**“我们的产品集成易观方舟SDK，易观方舟SDK可能需要收集您的设备Mac地址、唯一设备识别码（IMEI、android ID、IMSI 等信息）以提供统计分析服务”**

{% hint style="info" %}
1、sdk版本需要4.5.4以上

2、禁止数据采集后sdk不再采集数据和上报，会导致数据量下降；

3、如需恢复数据采集和上报，调用此接口参数传true即可，下次冷启动后才能恢复正常的数据采集和上报。
{% endhint %}

示例：

```java
// 用户没有同意隐私政策
if(privacyPolicyNotAllowed) {
    // 禁止数据采集和上报
    AnalysysAgent.setDataCollectEnable(false);
}
```

```java
// 用户同意隐私政策
if(privacyPolicyAllowed) {
    // 开启数据采集和上报，下次冷启动生效
    AnalysysAgent.setDataCollectEnable(true);
}
```

