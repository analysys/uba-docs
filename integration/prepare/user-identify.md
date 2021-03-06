# 如何准确识别用户

识别用户是一个比较复杂的过程，尤其是对于有帐号体系的产品来说，用户会有多种使用场景，可能会在匿名的情况下访问，也有可能在登录情况下使用，也有可能在同一台设备上登录不同的帐号，也可能同一个帐号在多台设备上登录。

因此，选择合适的用户标识有助于准确标识用户，提高分析的准确性。

## 1. 标识用户

方舟的事件模型中，数据上报时会有用户这个实体，使用 `xwho` 来进行标识。在登录前匿名阶段，`xwho` 中会记录一个匿名 ID ，登录后则应该调用 `alias` 方法传入 注册 ID。后续在方舟中就可通过这个注册ID来查询用户相关的行为了。

### 1.1 匿名 ID

匿名 ID 用来在用户主体未登录应用之前标识，当用户打开集成有方舟 SDK 的应用时，SDK 会给其分配一个 `UUID` 来做为匿名 ID 。

当然，方舟也提供了给用户主体设置匿名 ID 的方式，比如可以使用设备 ID ( iOS 的 IDFA/IDFV，Web 的 Cookie 等)。

### 1.2 注册 ID

通常是业务数据库里的主键或其它唯一标识，注册 ID 是更加精确的用户 ID，但很多应用不会用注册 ID，或者用户使用一些功能时是在未登录的状态下进行的，此时，就不会有注册 ID。

另外，在方舟系统中，我们以为用户主体来进行分析，这个用户主体可能是一个人，一个帐号，也可能是一个家电，一辆汽车。具体以什么做为用户主体，要根据用户实际的业务场景来决定。

### 1.3 distinct_id

即使有了 xwho（ 注册 ID / 匿名 ID)，实际使用中也会存在注册用户匿名访问等情况，所以需要一个唯一标识将用户行为贯穿起来，distinct_id 就是在 xwho 的基础上根据一些规则生成的唯一 ID。

## 2. 不同场景下选择不同的识别方案

实际接入分析的应用会有多种情况，可以分为两大类：

* **无帐号体系**，e.g. Snapseed、日历
*   **有帐号体系**

    ① 强帐号体系，必须登录 e.g. 钉钉、QQ、微信

    ② 强帐号体系，存在访客模式，关键转化需登录 e.g. 淘宝、微博、大众点评、招商银行

    ③ 弱帐号体系，存在访客模式，不登录不影响核心功能使用 e.g. 高德地图、今日头条、墨迹天气

### 2.1 无帐号体系 / 弱帐号体系且不分析登录用户的情况

在这种情况下，无需关心注册 ID，使用方舟的客户端 SDK 时，方舟的SDK会自动生成一个 **UUID** 作为匿名 ID，这个 **UUID** 会做为后续行为数据的匿名 ID（xwho），此时系统生成的 distinct_id 会与匿名 ID 一一对应，计算的用户数也会是 匿名的用户数。

当然，用户也可以通过调用 **identify** 接口来设置匿名 ID，比如使用设备唯一标识。

**identify** 接口格式如下：

```java
void identify(Context context, String xwho)
```

### 2.2 有帐号体系，需要分析注册用户和匿名用户的情况

这种情况下在集成时需要客户在用户进行登录 / 注册 / 完善个人资料等情况下调用 `alias` 接口获得注册 ID，使得匿名 ID 实名化，然后 SDK 就会将数据的 `$is_login` 属性变成 `true`，表示这是一个注册 ID，后续的行为中上报的`xwho`也会有注册ID。

> $is_login 用于标识是否是注册用户

但是实际会存在单用户多设备、单设备多用户、注册用户匿名访问等情况下，如何把每一条记录精准识别到各个用户上，贯通一个用户在一个设备上注册前后的行为，贯通一个注册用户在不同设备上登录之后的行为是个比较复杂的问题。

针对这种场景易观方舟提供了一种识别方案：

当调用 **alias** 接口之后，会将匿名 ID 和注册 ID 关联，后台算法根据一定的规则生成一个distinct_id，用于唯一标识用户，被绑定的匿名 ID 和注册 ID 发生的所有行为都会被认为是同一个用户实体发生的，在进行事件、漏斗、留存等用户相关的分析的时候也只会算作一个用户。

## 3. 原理说明

下面以一个实际的场景来说明用户识别的机制，其中：

发送的 `xwho`：登录前是匿名 ID ，登录后是注册 ID，调用 **alias** 接口时，两个 ID 会同时发送；

是否是注册 ID：当`xwho`为是否为一个注册 ID；

方舟 distinct_id：方舟内部给该用户分配的唯一标识，是用于计算触发用户数、漏斗、留存等的最终依据，对应自定义查询中 events 表中的 user_id 及 users 表中的 id 字段。

> 注意：在识别过程中，一个匿名 ID 只能和一个注册 ID 绑定，同样的一个注册 ID 也只能和一个匿名 ID 绑定。

| 行为顺序 | 发送的xwho         | 是否是注册 ID    | 方舟   distinct_id |
| ---- | --------------- | ----------- | ---------------- |
| 1    | X               | 否           | 1                |
| 2    | xiaozhou   -> X | ID   关联(成功) | 1                |
| 3    | xiaozhou        | 是           | 1                |
| 4    | xiaozhou        | 是           | 1                |
| 5    | dawang   -> X   | ID   关联(失败) | 2                |
| 6    | dawang          | 是           | 2                |
| 7    | Y               | 否           | 3                |
| 8    | xiaozhou   -> Y | ID   关联(失败) | 1                |
| 9    | xiaozhou        | 是           | 1                |
| 10   | dawang   -> Y   | ID   关联(失败) | 2                |

详细说明如下：

1. 某用户在小米手机上新安装了 App，匿名产生了一系列操作，SDK 生成的匿名 ID 为 X，对应分配的方舟 distinct_id 为 1；
2. 该用户进行了注册并登录，其注册 ID 为 xiaozhou，此时，需要调用 SDK 的 `alias` 接口，此时方舟会将匿名 ID X 与 注册 ID xiaozhou 进行成功关联；
3. 该用户在登录之后继续进行了一系列行为；
4. 该用户退出登录并进行了一系列的操作，SDK 不调用任何方法，此时方舟依然使用注册 ID xiaozhou 来标识当前用户；
5. 该用户使用一个已注册但未接入方舟系统的的帐号 dawang 来进行登录，此时方舟将尝试将 X 与 dawang 进行关联，由于 X 已经和 xiaozhou 关联，所以会关联失败，同时会分配一个新的方舟 distinct_id 为 2；
6. 该用户使用帐号 dawang 进行了一系列行为，这里方舟都使用注册 ID dawang来标识此用户；
7. 该用户更换了一个全新的苹果手机，并进行了一系列操作，由于尚未登录，此时方舟使用全新的匿名 ID Y 来标识此用户，对应分配的方舟 distinct_id 为 3；
8. 该用户在苹果手机上使用帐号 xiaozhou 进行登录，此时方舟将尝试将匿名 ID Y 与注册 ID xiaozhou进行关联，由于 xiaozhou 已经与 X 关联，因此会关联失败，但是依然会切换到以 xiaozhou 为注册 ID 的用户，其对应的方舟 distinct_id 依然为 1；
9. 该用户在苹果手机上的后续行为都以注册 ID xiaozhou来标识。

## 4. 使用前提

正确集成SDK，遵循接口的调用顺序，否则可能会导致部分用户标识异常，影响数据统计的正确性。

在 SDK 初始化完成之后，SDK 会自动生成一个 UUID 作为匿名用户标识，记录在 `xwho` 中，之后 SDK 采集上报的数据中 `$is_login` 属性为 `false`，来表示这是 匿名 ID 。

{% hint style="warning" %}
如果因业务要求需要对SDK生成的UUID进行调整,可以通过调用接口 **`identify`** 进行修改，接口使用方式请查看SDK指南。
{% endhint %}

当用户进行登录 / 注册 / 完善个人资料等会使得用户有 注册 ID 时的操作时，调用 `alias` 接口，上传匿名ID 和注册 ID 的关联关系。

**alias**接口格式如下：

```java
//Andorid SDK 示例，其中aliasId为您业务系统的ID
void alias(Context context, String aliasId)

```

当调用**alias**接口之后，接下来事件数据的 `$is_login` 属性都会被自动设置为`true`，表示事件是由一个注册 ID 触发的，后续行为事件中 `xwho` 都会是注册 ID。

在用户退出登录或者注销帐号时，如果想让匿名期间的行为归属到上一个登录用户时，可以不调用任何接口；反之，不想让匿名记录归属到上一个登录用户时，需要调用 **reset** 接口，之后方舟的 SDK 会自动生成一个 UUID 作为用户标识，上传到服务器时，会根据新生成一个distinct_id：

* 当下一个登录用户是首次注册，没被别的设备绑定时，匿名期间的用户就会归属到新用户上；
* 当下一个登录用户已经被其他设备绑定过时，匿名期间的用户行为就既不属于上一个用户也不属于下一个用户，只属于新生成的 UUID 这个匿名用户的行为。

**reset**接口格式如下：

```java
//Andorid SDK 示例 
void reset(Context context)
```

当调用**reset**接口之后，接下来事件数据的 `$is_login` 属性都会被自动设置为 `false`，表示事件是由一个匿名 ID 触发的。

## 5. 方案缺点

虽然该方案可以实现跨设备的用户贯通、以及准确的注册漏斗，但仍然存在局限性：

如果一个已注册用户（即已经和某个匿名 ID 关联过了）在一个新设备上进行操作，那么他在这个新设备的登录前行为是无法被准确识别的；

同样的，如果一个已注册的设备（即已经被关联到某个注册 ID了）上再次有新用户进行注册，也无法再次进行关联。

事实上，在比如如下的场景中，

1. 用户 xiaoming   登录后使用了一些功能后退出；
2. 匿名用户 X 访问；
3. 用户 dawang 登录使用

但匿名 X 到底是 xiaoming 还是 dawang ，或者是其他人都有可能，但是目前的方案还不能对全部场景做出准确判断。

{% hint style="info" %}
以上内容没有解答我的问题？[点击我进入方舟论坛去反馈](https://www.analysysdata.com/forum/index) 🚀
{% endhint %}
