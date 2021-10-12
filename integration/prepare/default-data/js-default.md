# JS 预置事件/属性

### **基础预置事件**

| 事件ID        | 属性ID                   | 数据类型 | 事件显示名称    | 事件说明                                            |
| ----------- | ---------------------- | ---- | --------- | ----------------------------------------------- |
| $startup    |                        |      | 启动        | 打开网站                                            |
|             | $is_first_time         | 布尔   | 是否安装后首次访问 | 是否安装后首次访问                                       |
|             | $预制属性                  |      |           | 其他预制通用属性                                        |
| $pageview   |                        |      | 浏览页面      | 浏览APP/网站页面                                      |
|             | $url                   | 字符串  | 页面URL(含参) | 页面完整路径                                          |
|             | $url_domain            | 字符串  | 页面URL（去参） | 去参的页面URL                                        |
|             | $title                 | 字符串  | 页面标题      | 页面标题                                            |
|             | $referrer              | 字符串  | 页面来源      | 页面来源（$referrer 字段在 App 中手动调用 pageview 接口，默认不采集） |
|             | $referrer_domain       | 字符串  | 页面来源域名    | 页面来源域名                                          |
|             | $预制属性                  |      |           | 其他预制通用属性                                        |
| $user_click |                        |      | 点击元素      | 全埋点自动采集元素点击行为                                   |
|             | $title                 | 字符串  | 页面标题      | 页面标题                                            |
|             | $url                   | 字符串  | 页面URL     | 页面URL                                           |
|             | $url_path              | 字符串  | 页面地址（不含参） | 页面地址（不含参）                                       |
|             | $element_path          | 字符串  | 元素路径      | APP 为元素唯一标识；JS 为元素路径                            |
|             | $element_class_name    | 字符串  | 元素样式的类    | 元素样式的类                                          |
|             | $element_target_url    | 字符串  | 元素链接地址    | 元素链接地址                                          |
|             | $element_id            | 字符串  | 元素ID      | 元素ID                                            |
|             | $element_name          | 字符串  | 元素名称      | 元素名称                                            |
|             | $element_type          | 字符串  | 元素类型      | 元素类型                                            |
|             | $element_position      | 字符串  | 列表控件位置    | 列表控件位置 （可选）                                     |
|             | $element_content       | 字符串  | 元素内容      | 元素的内容优先级：内容>描述>空                                |
|             | $预制属性                  |      |           | 其他预制通用属性                                        |
| $webstay    |                        |      | 视区停留      | 停留在可视区域（用于分析网页浏览深度                              |
|             | $url                   | 字符串  | 页面URL     | 页面URL/页面完整路径                                    |
|             | $title                 | 字符串  | 页面标题      | 页面标题                                            |
|             | $referrer              | 字符串  | 页面来源      | 页面来源                                            |
|             | $referrer_domain       | 字符串  | 页面来源域名    | 页面来源域名                                          |
|             | $viewport_width        | 字符串  | 视区宽度      | 视区宽度                                            |
|             | $viewport_position     | 数值   | 视区距顶部的位置  | 视区距顶部的位置                                        |
|             | $viewport_height       | 数值   | 视区高度      | 视区高度                                            |
|             | $event_duration        | 数值   | 视区停留时间    | 视区停留时间                                          |
| $web_click  |                        |      | App点击     | Web热图点击事件（用于热图分析）                               |
|             | $page_width            | 数值   | 页面宽度      | 热图页面宽度                                          |
|             | $page_height           | 数值   | 页面高度      | 热图页面高度                                          |
|             | $click_x               | 数值   | 点击X坐标     | 热图点击X坐标                                         |
|             | $click_y               | 数值   | 点击Y坐标     | 热图点击Y坐标                                         |
|             | $url                   | 字符串  | 页面URL     | 点击热图时页面URL                                      |
|             | $element_x             | 数值   | 元素X坐标     | 点击元素X坐标                                         |
|             | $element_y             | 数值   | 元素Y坐标     | 点击元素Y坐标                                         |
|             | $element_path          | 字符串  | 元素路径      | 热图元素路径                                          |
|             | $element_name          | 字符串  | 元素名称      | 热图元素名称                                          |
|             | $element_type          | 字符串  | 元素类型      | 热图元素类型                                          |
|             | $element_content       | 字符串  | 元素内容      | 热图元素的内容                                         |
|             | $element_clickable     | 数值   | 是否可以点击元素  | 是否可以点击元素                                        |
|             | $element_target_url    | 字符串  | 元素链接地址    | 元素链接地址                                          |
|             | $预制属性                  |      |           | 其他预制通用属性                                        |
| $alias      |                        |      |           |                                                 |
|             | $original_id           | 字符串  | 匿名ID      | 实名绑定前的匿名ID                                      |

### 预置事件通用属性

| 属性ID                | 属性显示名称     | 数据类型 | 属性说明                                                    |
| ------------------- | ---------- | ---- | ------------------------------------------------------- |
| $platform           | 平台         | 字符串  | 应用平台，枚举取值：JS/iOS/Android/Wechat                         |
| $manufacturer       | 设备制造商      | 字符串  | 制造厂商， e.g. 小米（通过UA解析）                                   |
| $brand              | 设备品牌       | 字符串  | 设备品牌，e.g. 华为荣耀（通过UA解析）                                  |
| $model              | 设备型号       | 字符串  | 设备型号，e.g. iPhone8、小米4（通过UA解析）                           |
| $os                 | 操作系统       | 字符串  | 操作系统，e.g.Window、MacOS（通过UA解析）                           |
| $os_version         | 操作系统版本     | 字符串  | 操作系统版本，e.g.Windows 10（通过UA解析）                           |
| $browser            | 浏览器        | 字符串  | 浏览器名称，e.g. Chrome（通过UA解析）                               |
| $browser_version    | 浏览器版本      | 字符串  | 浏览器版本，e.g. Chrome 62.23.23（通过UA解析）                      |
| $screen_width       | 屏幕宽度       | 数值   | 屏幕宽度/屏幕分辨率，e.g. 1920                                    |
| $screen_height      | 屏幕高度       | 数值   | 屏幕高度/屏幕分辨率，e.g. 768                                     |
| $is_login           | 是否是注册用户    | 布尔   | 是否是注册用户                                                 |
| $ip                 | IP         | 字符串  | <p></p><p>收数服务会自动记录上报的数据来源 IP，根据 IP 解析为国家、省份、城市三个字段</p> |
| $country            | 国家         | 字符串  | 默认根据用户IP解析获取,或用户手动上传覆盖                                  |
| $province           | 省份         | 字符串  | 默认根据用户IP解析获取,或用户手动上传覆盖                                  |
| $city               | 城市         | 字符串  | 默认根据用户IP解析获取,或用户手动上传覆盖                                  |
| $utm_campaign_id    | 活动ID       | 字符串  | <p>根据添加的内容自动生成，</p><p>标识一次活动</p>                        |
| $utm_campaign       | 活动/广告名称    | 字符串  | 特定的推广活动，e.g. 双11推广                                      |
| $utm_medium         | 活动/广告媒介    | 字符串  | 推广类型，e.g. SEM，cpc                                       |
| $utm_source         | 活动/广告来源    | 字符串  | 推广来源，e.g. 今日头条                                          |
| $utm_content        | 活动/广告内容    | 字符串  | 广告内容，e.g. 优惠信息                                          |
| $utm_term           | 活动/广告关键字   | 字符串  | 广告关键字，e.g. 用户画像                                         |
| $is_first_day       | 是否安装后首日访问  | 布尔   | 是否安装后首日访问                                               |
| $lib                | SDK类型      | 字符串  | SDK类型，e.g.   python、iOS等                                |
| $lib_version        | SDK版本      | 字符串  | SDK版本， e.g. ：11.2.5                                     |
| $session_id         | SessionID  | 字符串  | 会话ID，e.g. 515950b8f1a6221c                              |
| $language           | 语言         | 字符串  | 系统语言，e.g. zh-cn                                         |
| $time_zone          | 用户时区       | 字符串  | 用户时区，e.g.GMT+08:00                                      |
| $user_agent         | UA         | 字符串  | UA                                                      |
| $web_crawler        | 是否是爬虫      | 布尔   | 爬虫识别                                                    |
| $is_time_calibrated | 是否与服务端时间校准 | 布尔   | 是否与服务端时间校准                                              |
| $debug              | Debug模式    | 数值   | 标识数据处理方式，0：非debug 1：debug，不入库 2：debug，入库                |

### **预置用户通用属性**

| 属性ID                  | 属性名称       | 属性值数据类型 | 属性说明                    |
| --------------------- | ---------- | ------- | ----------------------- |
| $original_id          | 匿名ID       | 字符串     | 实名绑定前的匿名ID              |
| $phone                | 手机号        | 字符串     | 非自动采集，需要用户上传            |
| $email                | 邮箱         | 字符串     | 非自动采集，需要用户上传            |
| $platform             | 最后一次使用平台   | 字符串     | 最后一次使用平台                |
| $lib                  | 最新版本的SDK类型 | 字符串     | SDK类型，e.g.  python、iOS等 |
| $lib_version          | 最新版本的SDK版本 | 字符串     | SDK版本，e.g. 11.2.5       |
| $country              | 所在国家       | 字符串     | 默认根据用户IP解析获取,或用户手动上传覆盖  |
| $province             | 所在省份       | 字符串     | 默认根据用户IP解析获取,或用户手动上传覆盖  |
| $city                 | 所在城市       | 字符串     | 默认根据用户IP解析获取,或用户手动上传覆盖  |
| $is_login             | 是否是注册帐号    | 布尔值     | 是否是调用过alias接口           |
| $signup_time          | 注册时间       | 日期时间    | 注册时间                    |
| $first_visit_time     | 首次访问时间     | 日期时间    | 首次访问时间                  |
| $first_visit_language | 语言         | 字符串     | 设备语言                    |
| $time_zone            | 首次访问时区     | 字符串     | GMT+08:00               |
