# 预置事件和属性

为了帮助开发者更快速的集成SDK，了解采集哪些用户行为和属性，我们预置了一些事件、事件属性和用户属性。

{% hint style="info" %}
**说明**

部分默认自动采集，Android、iOS、JS 和 小程序端略有差异；

非默认采集的字段，如有需要，可以直接使用预置字段作为事件 ID、属性 ID 进行上报，以便数据集成时，能够自动生成预置看板。

以下表格中涉及标识为 Y/N/- 的含义

**事件**

* **Y 表示相应平台默认自动采集**
* **N 表示相应平台不默认采集**
* **S 表示由服务端处理**
* **-  表示相应平台不支持采集该事件**

**属性**

* **Y 表示采集事件后相应属性可以自动获取，无需额外配置**
* **N 表示需要额外配置才能有值**
* **S 表示由服务端根据相应规则自动处理**
* **-  表示相应平台不支持该属性**
{% endhint %}

{% hint style="danger" %}
除了预置的事件和属性ID会以$开头，其他自定义的事件ID和属性ID，须注意命名方式：仅支持字母、数字和下划线，不能以数字或下划线开头，上限125个半角字符。
{% endhint %}

## 预置事件

### 1. **Event：**基础预置事件

{% hint style="info" %}
基础预置事件会默认加入到方舟埋点方案

启动、关闭、浏览页面事件会在集成了基础 SDK 后会自动采集；

**$app_click**、**$web_click **用于记录点击网页/APP页面，用于分析点击位置热图、点击元素热图，集成 SDK 时设置参数_autoHeatmap _设置为 _true ；_

**$websta**y 用于记录用户停留在可视区域，分析浏览深度线，集成 SDK 时设置参数 _autoWebstay_ 为 _true；_

**$user_click** 用于采集用户点击元素的事件，集成 SDK 时开启全埋点功能，即设置参数 _autoTrack 为 true _

对于用不到的事件可以选择不用，比如集成的平台中没有小程序时，可以不用 $share；没有 APP 时，可以不用 $app_crash
{% endhint %}

| 事件ID        | 事件显示名称 | 事件说明                | Android | iOS |  JS | 小程序 |
| ----------- | ------ | ------------------- | :-----: | :-: | :-: | :-: |
| $startup    | 启动     | APP启动 / 打开网站        |    Y    |  Y  |  Y  |  Y  |
| $end        | 关闭     | APP关闭               |    Y    |  Y  |  -  |  -  |
| $pageview   | 浏览页面   | 浏览APP/网站页面          |    Y    |  Y  |  Y  |  Y  |
| $user_click | 点击元素   | 全埋点自动采集元素点击行为       |    N    |  N  |  N  |  N  |
| $app_click  | App点击  | App热图点击事件（用于热图分析）   |    N    |  N  |  -  |  -  |
| $web_click  | Web点击  | Web热图点击事件（用于热图分析）   |    -    |  -  |  N  |  -  |
| $webstay    | 视区停留   | 停留在可视区域（用于分析网页浏览深度） |    -    |  -  |  N  |  -  |
| $share      | 小程序分享  | 点击小程序分享按钮           |    -    |  -  |  -  |  N  |
| $app_crash  | APP崩溃  | APP崩溃信息             |    N    |  N  |  -  |  -  |

### 2. Event：APP 推广监测预置事件

{% hint style="info" %}
在首次创建 APP 推广监测成功后，系统会自动将 APP 推广监测相关事件添加在埋点方案中

无需在 SDK 中进行特殊设置，用户点击来推广链接激活后会自动上报数据
{% endhint %}

| 事件ID                | 事件显示名称  | 事件说明                         | Android | iOS | JS | 小程序 |
| ------------------- | ------- | ---------------------------- | ------- | --- | -- | --- |
| $campaign_track     | APP推广监测 | APP扫描监测扫描二维码时上报              | S       | S   | -  | -   |
| $first_installation | 首次安装激活  | APP扫描监测扫描二维码后首次打开APP会时上报激活事件 | S       | S   | -  | -   |

### 3. Event：消息通知预置事件

{% hint style="info" %}
在服务集成配置中配置消息通知推送通道后，系统会自动将这 3 个事件添加到埋点方案中

集成 SDK 时需要注意消息通知模块的设置，详见 [SDK 集成文档](https://docs.analysys.cn/integration/sdk/android/xiao-xi-tui-song-mo-kuai)
{% endhint %}

| 事件ID                   | 事件显示名称     | 事件说明         | Android | iOS |  JS | 小程序 |
| ---------------------- | ---------- | ------------ | :-----: | :-: | :-: | :-: |
| $push_receiver_success | 消息推送成功     | 设备收到推送消息时触发  |    N    |  N  |  -  |  -  |
| $push_click            | 点击推送消息     | 设备点击了推送消息时触发 |    N    |  N  |  -  |  -  |
| $push_process_success  | 成功处理push消息 | 成功处理push消息   |    N    |  N  |  -  |  -  |

#### 绑定用户实名信息

| 事件ID   | 事件显示名称   | 事件说明   | Android | iOS | JS | 小程序 |
| ------ | -------- | ------ | ------- | --- | -- | --- |
| $alias | 绑定用户实名信息 | 用户实名认证 | S       | S   | S  | S   |

###  4. Profile 系列事件

{% hint style="info" %}
$alias 事件之外的Profile 系列的事件用于上报用户属性，所以同样不会作为单独的事件去分析，即不会出现在分析模型中事件的选项中，也不会计入任意事件的计算。
{% endhint %}

| 事件ID               | 事件说明               | Android | iOS |  JS | 小程序 |
| ------------------ | ------------------ | :-----: | :-: | :-: | :-: |
| $alias             | 用户实名认证             |    N    |  N  |  N  |  N  |
| $profile_set       | 设置用户信息，覆盖写         |    N    |  N  |  N  |  N  |
| $profile_set_once  | 设置用户信息，有则不进行任何操作   |    Y    |  Y  |  Y  |  Y  |
| $profile_increment | 增加或减少用户信息中的数字类型的属性 |    N    |  N  |  N  |  N  |
| $profile_delete    | 删除用户信息             |    N    |  N  |  N  |  N  |
| $profile_append    | 数组属性添加值            |    N    |  N  |  N  |  N  |
| $profile_unset     | 设置用户信息中的某个属性为空     |    N    |  N  |  N  |  N  |

{% hint style="warning" %}
除了上述预置事件之外，更多业务相关的事件，需要自定义埋点上报。
{% endhint %}

{% content-ref url="../../../features/project-manegement/data-integration/schema.md" %}
[schema.md](../../../features/project-manegement/data-integration/schema.md)
{% endcontent-ref %}

## 预置 Event 事件通用属性

事件属性描述事件发生的方式和内容，是分析过程中的维度，也可以用于条件过滤。

* 事件通用属性：所有事件共同拥有的属性，e.g. 平台、应用版本、操作系统等；
* 事件自有属性：某个事件独有的事件属性，e.g. 浏览页面事件 $pageview 会有 $url、$title 等属性。

| 属性ID                | 属性显示名称     | 数据类型 | 属性说明                                                       | Android | iOS |  JS | 小程序 |
| ------------------- | ---------- | ---- | ---------------------------------------------------------- | :-----: | :-: | :-: | :-: |
| $platform           | 平台         | 字符串  | 应用平台，枚举取值：JS/iOS/Android/Wechat                            |    Y    |  Y  |  Y  |  Y  |
| $app_version        | 应用版本       | 字符串  | 应用版本，e.g. V1.0                                             |    Y    |  Y  |  -  |  -  |
| $device_type        | 设备类型       | 字符串  | 设备类型，e.g.  PC、移动设备                                         |    S    |  S  |  S  |  S  |
| $manufacturer       | 设备制造商      | 字符串  | 制造厂商， e.g. 小米                                              |    Y    |  Y  |  -  |  -  |
| $brand              | 设备品牌       | 字符串  | 设备品牌，e.g. 华为荣耀                                             |    Y    |  Y  |  S  |  Y  |
| $model              | 设备型号       | 字符串  | 设备型号，e.g. iPhone8、小米4                                      |    Y    |  Y  |  S  |  Y  |
| $os                 | 操作系统       | 字符串  | 操作系统，e.g.Window、MacOS                                      |    Y    |  Y  |  S  |  Y  |
| $os_version         | 操作系统版本     | 字符串  | 操作系统版本，e.g.Windows 10                                      |    Y    |  Y  |  S  |  Y  |
| $browser            | 浏览器        | 字符串  | 浏览器名称，e.g. Chrome                                          |    -    |  -  |  S  |  Y  |
| $browser_version    | 浏览器版本      | 字符串  | 浏览器版本，e.g. Chrome 62.23.23                                 |    -    |  -  |  S  |  Y  |
| $network            | 网络类型       | 字符串  | 网络类型，e.g. WIFI、2G、3G、4G                                    |    Y    |  Y  |  -  |  Y  |
| $carrier_name       | 运营商        | 字符串  | 接入运营商名称，e.g. 中国联通                                          |    Y    |  Y  |  -  |  -  |
| $screen_width       | 屏幕宽度       | 数值   | 屏幕宽度/屏幕分辨率，e.g. 1920                                       |    Y    |  Y  |  Y  |  Y  |
| $screen_height      | 屏幕高度       | 数值   | 屏幕高度/屏幕分辨率，e.g. 768                                        |    Y    |  Y  |  Y  |  Y  |
| $is_login           | 是否是注册用户    | 布尔   | 是否是注册用户                                                    |    Y    |  Y  |  Y  |  Y  |
| $ip                 | IP         | 字符串  | IP地址                                                       |    S    |  S  |  S  |  S  |
| $country            | 国家         | 字符串  | <p>事件发生时所在国家，</p><p>e.g. 中国、美国</p>                         |    S    |  S  |  S  |  S  |
| $province           | 省份         | 字符串  | <p>事件发生时所在省份，</p><p>e.g.   北京、上海、福建</p>                    |    S    |  S  |  S  |  S  |
| $city               | 城市         | 字符串  | <p>事件发生时所在城市，</p><p>e.g. 北京、厦门</p>                         |    S    |  S  |  S  |  S  |
| $utm_campaign_id    | 活动ID       | 字符串  | <p>根据添加的内容自动生成，</p><p>标识一次活动</p>                           |    Y    |  Y  |  Y  |  Y  |
| $utm_campaign       | 活动/广告名称    | 字符串  | 特定的推广活动，e.g. 双11推广                                         |    Y    |  Y  |  Y  |  Y  |
| $utm_medium         | 活动/广告媒介    | 字符串  | 推广类型，e.g. SEM，cpc                                          |    Y    |  Y  |  Y  |  Y  |
| $utm_source         | 活动/广告来源    | 字符串  | 推广来源，e.g. 今日头条                                             |    Y    |  Y  |  Y  |  Y  |
| $utm_content        | 活动/广告内容    | 字符串  | 广告内容，e.g. 优惠信息                                             |    Y    |  Y  |  Y  |  Y  |
| $utm_term           | 活动/广告关键字   | 字符串  | 广告关键字，e.g. 用户画像                                            |    Y    |  Y  |  Y  |  Y  |
| $is_first_day       | 是否安装后首日访问  | 布尔   | 是否安装后首日访问                                                  |    Y    |  Y  |  Y  |  Y  |
| $channel            | 下载渠道       | 字符串  | 下载渠道，SDK 初始化时传入。仅 Android 通过渠道包分发时才有意义，iOS 会统一为“App Store” |    Y    |  Y  |  -  |  -  |
| $lib                | SDK类型      | 字符串  | SDK类型，e.g.   python、iOS等                                   |    Y    |  Y  |  Y  |  Y  |
| $lib_version        | SDK版本      | 字符串  | SDK版本， e.g. ：11.2.5                                        |    Y    |  Y  |  Y  |  Y  |
| $session_id         | SessionID  | 字符串  | 会话ID，e.g. 515950b8f1a6221c                                 |    Y    |  Y  |  Y  |  Y  |
| $language           | 语言         | 字符串  | 系统语言，e.g. zh-cn                                            |    Y    |  Y  |  Y  |  Y  |
| $time_zone          | 用户时区       | 字符串  | 用户时区，e.g.GMT+08:00                                         |    Y    |  Y  |  Y  |  Y  |
| $user_agent         | UA         | 字符串  | UA                                                         |    -    |  -  |  Y  |  -  |
| $web_crawler        | 是否是爬虫      | 布尔   | 爬虫识别                                                       |    -    |  -  |  Y  |  -  |
| $is_time_calibrated | 是否与服务端时间校准 | 布尔   | 是否与服务端时间校准                                                 |    N    |  N  |  -  |  N  |
| $device_id          | 设备ID       | 字符串  | 设备ID，idfa/oaid > idfv/androidid > uuid                     |    N    |  N  |  -  |  -  |
| xwho                | 用户ID       | 字符串  | 用户ID                                                       |    Y    |  Y  |  Y  |  Y  |
| xwhen               | 触发时间       | 日期   | 事件发生的时间                                                    |    Y    |  Y  |  Y  |  Y  |
| distinct_id         | 唯一ID       | 字符串  | 系统在 xwho 的基础上根据一些规则生成的唯一 IDS                               |    S    |  S  |  S  |  S  |
| $importflag         | 是否工具导入     | 数值   | 标识是否是工具导入，1为工具导入                                           |    N    |  N  |  N  |  N  |
| $debug              | Debug模式    | 数值   | 标识数据处理方式，0：非debug 1：debug，不入库 2：debug，入库                   |    Y    |  Y  |  Y  |  Y  |

{% hint style="info" %}
**非自动采集的属性，会根据相应字段自动解析**

**$ip ：**方舟的收数服务会自动记录上报的数据来源 IP，根据 IP 解析为国家、省份、城市三个字段

**$county：**通过 IP 解析

**$province：**通过 IP 解析

**$city ：**通过 IP 解析

**$device_type：**通过 UA 解析
{% endhint %}

{% hint style="info" %}
**部分自动采集的属性不会作为独立的属性用于分析**

**$debug：**用于标识是否入库

* 0：表示关闭 Debug 模式
* 1：表示打开 Debug 模式，但该模式下发送的数据仅用于调试，不计入平台数据统计 
* 2：表示打开 Debug 模式，该模式下发送的数据可计入平台数据统计

**$session_id：**标识一次会话

**$user_agent：**UA，用于解析设备类型、浏览器、浏览器版本、操作系统、操作系统版本\
\
**$device_id：系统唯一标识，默认不采集(4.4.5版本新增)**

**Andorid 采集规则：**advertising id > android id > uuid，按照先后顺序获取

**iOS 采集规则：**idfa>idfv>uuid，按照先后顺序获取
{% endhint %}

## 预置 Event 事件自身属性

部分预置事件在通用属性之外，还有自身独有的属性

###  1 基础预置事件

### **$startup 启动**

{% hint style="info" %}
集成基础 SDK 后自动采集
{% endhint %}

| 属性ID                | 属性显示名称    | 数据类型 | 属性说明                                          | Android | iOS |  JS | 小程序 |
| ------------------- | --------- | ---- | --------------------------------------------- | :-----: | :-: | :-: | :-: |
| $is_first_time      | 是否安装后首次访问 | 布尔   | 是否安装后首次访问                                     |    Y    |  Y  |  Y  |  Y  |
| $is_from_background | 是否从后台唤醒   | 布尔   | 是否从后台唤醒恢复                                     |    Y    |  Y  |  -  |  -  |
| $start_source       | 启动来源      | 字符串  | 标识APP的启动来源，e.g. 通过点击图标启动、点击通知、URL唤醒、3D touch等 |    N    |  N  |  -  |  -  |
| $scene              | 场景值       | 字符串  | 标识小程序的场景值，e.g 顶部搜索框的搜索结果页                     |    -    |  -  |  -  |  Y  |
| $scene_type         | 场景值类型     | 字符串  | 标识小程序场景值类型                                    |    -    |  -  |  -  |  S  |

### **$end 关闭**

{% hint style="info" %}
**集成基础 SDK 后自动采集**
{% endhint %}

| 属性ID      | 属性显示名称 | 数据类型 | 属性说明                        | Android | iOS |  JS | 小程序 |
| --------- | ------ | ---- | --------------------------- | :-----: | :-: | :-: | :-: |
| $duration | 使用时长   | 数值   | <p>从启动到关闭的使用时长<br>单位：毫秒</p> |    Y    |  Y  |  -  |  -  |

### **$pageview 浏览页面**

{% hint style="info" %}
**集成基础 SDK 后自动采集**
{% endhint %}

| 属性ID                 | 属性显示名称    | 数据类型 | 属性说明                      | Android | iOS |  JS | 小程序 |
| -------------------- | --------- | ---- | ------------------------- | :-----: | :-: | :-: | :-: |
| $url                 | 页面URL(含参) | 字符串  | 页面完整路径                    |    Y    |  Y  |  Y  |  Y  |
| $url_domain          | 页面URL     | 字符串  | 去参的页面URL                  |    -    |  -  |  S  |  -  |
| $title               | 页面标题      | 字符串  | 页面标题                      |    Y    |  Y  |  Y  |  -  |
| $referrer            | 页面来源      | 字符串  | 页面来源                      |    Y    |  Y  |  Y  |  Y  |
| $referrer_domain     | 页面来源域名    | 字符串  | 页面来源域名                    |    -    |  -  |  Y  |  -  |
| $traffic_source_type | 流量来源类型    | 字符串  | 流量来源类型，数据处理               |    -    |  -  |  S  |  -  |
| $search_engine       | 搜索引擎      | 字符串  | 标识搜索引擎来源，e.g. 百度          |    -    |  -  |  S  |  -  |
| $search_keyword      | 搜索关键词     | 字符串  | 标识搜索词来源，e.g. 易观方舟         |    -    |  -  |  S  |  -  |
| $social_media        | 社交媒体      | 字符串  | 标识社交媒体来源，e.g. 微博          |    -    |  -  |  S  |  -  |
| $social_share_from   | 社交媒体分享来源  | 字符串  | 标识微信来源，e.g. 微信朋友圈、微信群     |    -    |  -  |  S  |  -  |
| $scene               | 场景值       | 字符串  | 标识小程序的场景值，e.g 顶部搜索框的搜索结果页 |    -    |  -  |  -  |  Y  |
| $scene_type          | 场景值类型     | 字符串  | 标识小程序场景值类型                |    -    |  -  |  -  |  S  |
| $startup_time        | 启动时间      | 日期   | yyyy-MM-dd hh:mm:ss.SSS   |    -    |  -  |  Y  |  Y  |
| $share_id            | 分享者ID     | 字符串  | 当点击分享的小程序后上报来源            |    -    |  -  |  -  |  N  |
| $share_level         | 转发层级      | 数值   | 当点击分享的小程序后上报来源            |    -    |  -  |  -  |  N  |
| $share_path          | 转发地址      | 字符串  | 当点击分享的小程序后上报来源            |    --   |  -  |  -  |  N  |

{% hint style="info" %}
* **$referrer 字段在 App 中手动调用 pageview 接口，默认不采集**
* **$url_domain, $traffic_source_type, $search_engine 等非自动采集的属性，系统会根据$url 和 $referrer 自动解析**
{% endhint %}

### **$user_click 点击元素（全埋点事件）**

{% hint style="info" %}
用于采集用户点击元素的事件，集成 SDK 时需开启全埋点功能，即设置参数 _autoTrack 为 true _

标识为 N 的属性表示设置参数 _autoTrack 为 true  _后，相应属性也需要额外配置
{% endhint %}

| 属性ID                   | 属性显示名称       | 数据类型 | 属性说明                 | Android | iOS |  JS | 小程序 |
| ---------------------- | ------------ | ---- | -------------------- | :-----: | :-: | :-: | :-: |
| $title                 | 页面标题         | 字符串  | 页面标题                 |    Y    |  Y  |  Y  |  -  |
| $parent_url            | 父页面URL       | 字符串  | 页面URL，为空则为顶级页        |    Y    |  -  |  -  |  -  |
| $url                   | 页面URL        | 字符串  | 页面URL                |    Y    |  Y  |  Y  |  Y  |
| $url_path              | 页面地址（不含参）    | 字符串  | 页面地址（不含参）            |    -    |  -  |  Y  |  -  |
| $element_path          | 元素路径         | 字符串  | APP 为元素唯一标识；JS 为元素路径 |    Y    |  Y  |  Y  |  -  |
| $element_class_name    | 元素样式的类       | 字符串  | 仅 JS 有效              |    -    |  -  |  Y  |  -  |
| $element_target_url    | 元素链接地址       | 字符串  | 仅 JS 有效              |    -    |  -  |  Y  |  -  |
| $element_id            | 元素ID         |  字符串 | 元素ID                 |    Y    |  Y  |  Y  |  N  |
| $element_name          | 元素名称         | 字符串  | 仅 JS 有效              |    -    |  -  |  Y  |  -  |
| $element_type          | 元素类型         | 字符串  | 元素类型                 |    Y    |  Y  |  Y  |  N  |
| $element_position      |  列表控件位置 （可选） | 字符串  | 列表控件位置 （可选）          |    Y    |  Y  |  -  |  -  |
| $element_content       | 元素内容         | 字符串  | 元素的内容（优先级：内容>描述>空）   |    Y    |  Y  |  Y  |  N  |

### **$webstay 视区停留**

{% hint style="info" %}
采集用户在可视区域的停留行为，分析浏览深度线，集成 SDK 时设置参数 _autoWebstay_ 为 _true_
{% endhint %}

| 属性ID               | 属性显示名称   | 数据类型 | 属性说明         | Android | iOS |  JS | 小程序 |
| ------------------ | -------- | ---- | ------------ | :-----: | :-: | :-: | :-: |
| $url               | 页面URL    | 字符串  | 页面URL/页面完整路径 |    -    |  -  |  Y  |  -  |
| $title             | 页面标题     | 字符串  | 页面标题         |    -    |  -  |  Y  |  -  |
| $referrer          | 页面来源     | 字符串  | 页面来源         |    -    |  -  |  Y  |  -  |
| $referrer_domain   | 页面来源域名   | 字符串  | 页面来源域名       |    -    |  -  |  Y  |  -  |
| $viewport_width    | 视区宽度     | 数值   | 视区宽度         |    -    |  -  |  Y  |  -  |
| $viewport_position | 视区距顶部的位置 | 数值   | 视区距顶部的位置     |    -    |  -  |  Y  |  -  |
| $viewport_height   | 视区高度     | 数值   | 视区高度         |    -    |  -  |  Y  |  -  |
| $event_duration    | 视区停留时间   | 数值   | 视区停留时间       |    -    |  -  |  Y  |  -  |

### **$app_click APP点击**

{% hint style="info" %}
采集APP点击行为，用于分析点击位置热图、点击元素热图，集成 SDK 时设置参数_autoHeatmap _设置为 _true _
{% endhint %}

| 属性ID               | 属性显示名称   | 数据类型 | 属性说明       | Android | iOS |  JS | 小程序 |
| ------------------ | -------- | ---- | ---------- | :-----: | :-: | :-: | :-: |
| $page_width        | 页面宽度     | 数值   | 热图页面宽度     |    Y    |  Y  |  Y  |  -  |
| $page_height       | 页面高度     | 数值   | 热图页面高度     |    Y    |  Y  |  Y  |  -  |
| $screen_dpi        | 屏幕DPI    | 数值   | 屏幕DPI      |    Y    |  -  |  -  |  -  |
| $screen_scale      | 屏幕缩放比    | 数值   | 屏幕缩放比      |    Y    |  -  |  -  |  -  |
| $click_x           | 点击X坐标    | 数值   | 热图点击X坐标    |    Y    |  Y  |  Y  |  -  |
| $click_y           | 点击Y坐标    | 数值   | 热图点击Y坐标    |    Y    |  Y  |  Y  |  -  |
| $url               | 页面URL    | 字符串  | 点击热图时页面URL |    Y    |  Y  |  Y  |  -  |
| $element_x         | 元素X坐标    | 数值   | 点击元素X坐标    |    Y    |  Y  |  Y  |  -  |
| $element_y         | 元素Y坐标    | 数值   | 点击元素Y坐标    |    Y    |  Y  |  Y  |  -  |
| $element_path      | 元素路径     | 字符串  | 热图元素路径     |    Y    |  Y  |  Y  |  -  |
| $element_name      | 元素名称     | 字符串  | 热图元素名称     |    -    |  Y  |  -  |  -  |
| $element_type      | 元素类型     | 字符串  | 热图元素类型     |    Y    |  Y  |  Y  |  -  |
| $element_content   | 元素内容     | 字符串  | 热图元素的内容    |    Y    |  Y  |  Y  |  -  |
| $element_clickable | 是否可以点击元素 | 数值   | 是否可以点击元素   |    Y    |  Y  |  Y  |  -  |

### **$web_click  Web点击**

{% hint style="info" %}
采集网页点击行为，用于分析点击位置热图、点击元素热图，集成 SDK 时设置参数_autoHeatmap _设置为 _true _
{% endhint %}

| 属性ID                   | 属性显示名称   | 数据类型 | 属性说明       | Android | iOS |  JS | 小程序 |
| ---------------------- | -------- | ---- | ---------- | :-----: | :-: | :-: | :-: |
| $page_width            | 页面宽度     | 数值   | 热图页面宽度     |    Y    |  Y  |  Y  |  -  |
| $page_height           | 页面高度     | 数值   | 热图页面高度     |    Y    |  Y  |  Y  |  -  |
| $screen_dpi            | 屏幕DPI    | 数值   | 屏幕DPI      |    Y    |  -  |  -  |  -  |
| $screen_scale          | 屏幕缩放比    | 数值   | 屏幕缩放比      |    Y    |  -  |  -  |  -  |
| $click_x               | 点击X坐标    | 数值   | 热图点击X坐标    |    Y    |  Y  |  Y  |  -  |
| $click_y               | 点击Y坐标    | 数值   | 热图点击Y坐标    |    Y    |  Y  |  Y  |  -  |
| $url                   | 页面URL    | 字符串  | 点击热图时页面URL |    Y    |  Y  |  Y  |  -  |
| $element_x             | 元素X坐标    | 数值   | 点击元素X坐标    |    Y    |  Y  |  Y  |  -  |
| $element_y             | 元素Y坐标    | 数值   | 点击元素Y坐标    |    Y    |  Y  |  Y  |  -  |
| $element_path          | 元素路径     | 字符串  | 热图元素路径     |    Y    |  Y  |  Y  |  -  |
| $element_name          | 元素名称     | 字符串  | 热图元素名称     |    -    |  Y  |  -  |  -  |
| $element_type          | 元素类型     | 字符串  | 热图元素类型     |    Y    |  Y  |  Y  |  -  |
| $element_content       | 元素内容     | 字符串  | 热图元素的内容    |    Y    |  Y  |  Y  |  -  |
| $element_clickable     | 是否可以点击元素 | 数值   | 是否可以点击元素   |    Y    |  Y  |  Y  |  -  |
| $element_target_url    | 元素链接地址   | 字符串  | 仅 JS 有效    |    -    |  -  |  Y  |  -  |

### **$share 小程序分享**

| 属性ID         | 属性显示名称 | 数据类型 | 属性说明           | Android | iOS |  JS | 小程序 |
| ------------ | ------ | ---- | -------------- | :-----: | :-: | :-: | :-: |
| $share_id    | 分享者ID  | 字符串  | 当点击分享的小程序后上报来源 |    -    |  -  |  -  |  N  |
| $share_level | 转发层级   | 数值   | 当点击分享的小程序后上报来源 |    -    |  -  |  -  |  N  |
| $share_path  | 转发地址   | 字符串  | 当点击分享的小程序后上报来源 |    -    |  -  |  -  |  N  |

### $app_crash APP崩溃

| 属性ID        | 属性显示名称 | 数据类型 | 属性说明    | Android | iOS |  JS | 小程序 |
| ----------- | ------ | ---- | ------- | :-----: | :-: | :-: | :-: |
| $crash_data | 崩溃原因   | 字符串  | 崩溃的堆栈信息 |    Y    |  Y  |  -  |  -  |

### **$alias  实名绑定**

| 属性ID         | 属性显示名称 | 数据类型 | 属性说明       | Android | iOS |  JS | 小程序 |
| ------------ | ------ | ---- | ---------- | :-----: | :-: | :-: | :-: |
| $original_id | 匿名ID   | 字符串  | 实名绑定前的匿名ID |    Y    |  Y  |  Y  |  Y  |

### 2 APP 推广监测预置事件

### $campaign_track APP推广监测

| 属性ID                | 属性名称       | 属性值数据类型 | 属性说明            | <p>Android<br>自动采集</p> | <p>iOS<br>自动采集</p> | <p>JS<br>自动采集</p> | <p>小程序<br>自动采集</p> |
| ------------------- | ---------- | ------- | --------------- | ---------------------- | ------------------ | ----------------- | ------------------ |
| $campaign_channelid | 推广渠道ID     | 数值      | APP推广监测扫描二维码时上报 | Y                      | Y                  | -                 | -                  |
| $campaign_shortlink | 推广跳转短链CODE | 字符串     | APP推广监测扫描二维码时上报 | Y                      | Y                  | -                 | -                  |
| $prop\_0            | 推广渠道信息1    | 字符串     | APP推广监测扫描二维码时上报 | Y                      | Y                  | -                 | -                  |
| $prop\_1            | 推广渠道信息2    | 字符串     | APP推广监测扫描二维码时上报 | Y                      | Y                  | -                 | -                  |
| $prop\_2            | 推广渠道信息3    | 字符串     | APP推广监测扫描二维码时上报 | Y                      | Y                  | -                 | -                  |
| $prop\_3            | 推广渠道信息4    | 字符串     | APP推广监测扫描二维码时上报 | Y                      | Y                  | -                 | -                  |
| $prop\_4            | 推广渠道信息5    | 字符串     | APP推广监测扫描二维码时上报 | Y                      | Y                  | -                 | -                  |

### $first_installation 首次安装激活

| 属性ID         | 属性名称 | 属性值数据类型 | 属性说明     | <p>Android<br>自动采集</p> | <p>iOS<br>自动采集</p> | <p>JS<br>自动采集</p> | <p>小程序<br>自动采集</p> |
| ------------ | ---- | ------- | -------- | ---------------------- | ------------------ | ----------------- | ------------------ |
| $fingerprint | 设备指纹 | 数值      | 设备指纹     | S                      | S                  | -                 | -                  |
| $track_xwhen | 激活时间 | 数值      | 指纹匹配上的时间 | S                      | S                  | -                 | -                  |

####

### 3 消息通知预置事件

### **$push_receiver_success 消息推送成功**

| 属性ID         | 属性显示名称 | 数据类型 | 属性说明         | Android | iOS |  JS | 小程序 |
| ------------ | ------ | ---- | ------------ | :-----: | :-: | :-: | :-: |
| $action_type | 操作类型   | 数值   | 点击消息通知后的操作类型 |    N    |  N  |  -  |  -  |
| $action      | 操作     | 字符串  | 点击消息通知后的操作   |    N    |  N  |  -  |  -  |

### **$push_process_success 成功处理消息**

| 属性ID         | 属性显示名称 | 数据类型 | 属性说明         | Android | iOS |  JS | 小程序 |
| ------------ | ------ | ---- | ------------ | :-----: | :-: | :-: | :-: |
| $action_type | 操作类型   | 数值   | 点击消息通知后的操作类型 |    N    |  N  |  -  |  -  |
| $action      | 操作     | 字符串  | 点击消息通知后的操作   |    N    |  N  |  -  |  -  |

### **$push_click 点击消息通知**

| 属性ID         | 属性显示名称 | 数据类型 | 属性说明         | Android | iOS |  JS | 小程序 |
| ------------ | ------ | ---- | ------------ | :-----: | :-: | :-: | :-: |
| $action_type | 操作类型   | 数值   | 点击消息通知后的操作类型 |    N    |  N  |  -  |  -  |
| $action      | 操作     | 字符串  | 点击消息通知后的操作   |    N    |  N  |  -  |  -  |

## 预置用户属性

### **基础预置用户属性**

{% hint style="info" %}
默认加入到方舟埋点方案-用户方案中
{% endhint %}

| 属性ID                  | 属性名称       | 属性值数据类型 | 属性说明                    | <p>Android<br>自动采集</p> | <p>iOS<br>自动采集</p> | <p>JS<br>自动采集</p> | <p>小程序<br>自动采集</p> |
| --------------------- | ---------- | ------- | ----------------------- | ---------------------- | ------------------ | ----------------- | ------------------ |
| distinct_id           | 唯一ID       | 数值      | 方舟系统生成的用户唯一ID           | S                      | S                  | S                 | S                  |
| xwho                  | 用户ID       | 字符串     | 行为主体                    | Y                      | Y                  | Y                 | Y                  |
| xwhen                 | 用户属性更新时间   | 日期时间    | 用户属性更新时间                | Y                      | Y                  | Y                 | Y                  |
| $original_id          | 匿名ID       | 字符串     | 实名绑定前的匿名ID              | S                      | S                  | S                 | S                  |
| $original_id_list     | 匿名ID列表     | 字符串     | 实名绑定过的匿名ID列表            | S                      | S                  | S                 | S                  |
| $idfv                 | IDFV       | 字符串     | IDFV                    | -                      | N                  | -                 | -                  |
| $idfa                 | IDFA       | 字符串     | IDFA                    | -                      | N                  | -                 | -                  |
| $mac                  | MAC        | 字符串     | MAC                     | N                      | -                  | -                 | -                  |
| $device_id            | DeviceID   | 字符串     | DeviceID                | N                      | N                  |                   |                    |
| $imei                 | IMEI       | 字符串     | IMEI                    | N                      | -                  | -                 | -                  |
| $wechatopenid         | 微信OpenID   | 字符串     | 微信OpenID                | -                      | -                  | -                 | N                  |
| $phone                | 手机号        | 字符串     | 手机号                     | N                      | N                  | N                 | N                  |
| $email                | 邮箱         | 字符串     | 邮箱                      | N                      | N                  | N                 | N                  |
| $platform             | 最后一次使用平台   | 字符串     | 最后一次使用平台                | Y                      | Y                  | Y                 | Y                  |
| $lib                  | 最新版本的SDK类型 | 字符串     | SDK类型，e.g.  python、iOS等 | Y                      | Y                  | Y                 | Y                  |
| $lib_version          | 最新版本的SDK版本 | 字符串     | SDK版本，e.g. 11.2.5       | Y                      | Y                  | Y                 | Y                  |
| $country              | 所在国家       | 字符串     | 用户所在国家                  | N                      | N                  | N                 | N                  |
| $province             | 所在省份       | 字符串     | 用户所在省份                  | N                      | N                  | N                 | N                  |
| $city                 | 所在城市       | 字符串     | 用户所在城市                  | N                      | N                  | N                 | N                  |
| $is_login             | 是否是注册帐号    | 布尔值     | 是否是注册帐号                 | Y                      | Y                  | Y                 | Y                  |
| $signup_time          | 注册时间       | 日期时间    | 注册时间                    | N                      | N                  | N                 | N                  |
| $first_visit_time     | 首次访问时间     | 日期时间    | 首次访问时间                  | Y                      | Y                  | Y                 | Y                  |
| $first_visit_language | 首次访问语言     | 字符串     | 设备语言                    | Y                      | Y                  | Y                 | Y                  |
| $time_zone            | 时区         | 字符串     | GMT+08:00               | Y                      | Y                  | Y                 | Y                  |

### **推送相关用户属性**

{% hint style="info" %}
集成服务配置/EA配置后注册
{% endhint %}

| 属性ID    | 属性名称   | 属性值数据类型 | 属性说明     | <p>Android<br>自动采集</p> | <p>iOS<br>自动采集</p> | <p>JS<br>自动采集</p> | <p>小程序<br>自动采集</p> |
| ------- | ------ | ------- | -------- | ---------------------- | ------------------ | ----------------- | ------------------ |
| $getui  | 个推ID   | 字符串     | 个推推送ID   | N                      | N                  | -                 | -                  |
| $jpush  | 极光ID   | 字符串     | 极光推送ID   | N                      | N                  | -                 | -                  |
| $baidu  | 百度ID   | 字符串     | 百度推送ID   | N                      | N                  | -                 | -                  |
| $xiaomi | 小米ID   | 字符串     | 小米推送ID   | N                      | N                  | -                 | -                  |
| $huawei | 华为ID   | 字符串     | 华为推送ID   | N                      | -                  | -                 | -                  |
| $aliyun | 阿里云ID  | 字符串     | 阿里云推送ID  | N                      | N                  | N                 | N                  |
| $xinge  | 信鸽ID   | 字符串     | 信鸽推送ID   | N                      | N                  | N                 | N                  |
| $apns   | ANPS   | 字符串     | ANPS     | -                      | N                  | -                 | -                  |
| $meizu  | 魅族ID   | 字符串     | 魅族推送ID   | N                      | -                  | -                 | -                  |
| $oppo   | OPPOID | 字符串     | OPPO推送ID | N                      | -                  | -                 | -                  |
| $vivo   | VIVOID | 字符串     | VIVO推送ID | N                      | -                  | -                 | -                  |

### 渠道监测相关用户属性

{% hint style="info" %}
首次创建APP推广监测成功时触发注册
{% endhint %}

| 属性ID                | 属性名称       | 属性值数据类型 | 属性说明            | <p>Android<br>自动采集</p> | <p>iOS<br>自动采集</p> | <p>JS<br>自动采集</p> | <p>小程序<br>自动采集</p> |
| ------------------- | ---------- | ------- | --------------- | ---------------------- | ------------------ | ----------------- | ------------------ |
| $prop\_0            | 推广渠道信息1    | 字符串     | APP推广监测扫描二维码时上报 | Y                      | Y                  | -                 | -                  |
| $prop\_1            | 推广渠道信息2    | 字符串     | APP推广监测扫描二维码时上报 | Y                      | Y                  | -                 | -                  |
| $prop\_2            | 推广渠道信息3    | 字符串     | APP推广监测扫描二维码时上报 | Y                      | Y                  | -                 | -                  |
| $prop\_3            | 推广渠道信息4    | 字符串     | APP推广监测扫描二维码时上报 | Y                      | Y                  | -                 | -                  |
| $prop\_4            | 推广渠道信息5    | 字符串     | APP推广监测扫描二维码时上报 | Y                      | Y                  | -                 | -                  |
| $campaign_shortlink | 推广跳转短链CODE | 字符串     | APP推广监测扫描二维码时上报 | Y                      | Y                  | -                 | -                  |
| $campaign_channelid | 推广渠道ID     | 数值      | APP推广监测扫描二维码时上报 | Y                      | Y                  | -                 | -                  |

{% hint style="info" %}
以上内容没有解答我的问题？[点击我进入方舟论坛去反馈](https://www.analysysdata.com/forum/index) 🚀
{% endhint %}
