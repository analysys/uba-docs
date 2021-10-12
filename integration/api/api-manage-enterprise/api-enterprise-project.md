# 项目管理

## 1. 获取项目列表

### 1.1 接口地址

> 【GET】 /uba/manage/enterprise/projects

### 1.2 请求参数示例

无

> **认证参数**：接口必传 xtoken 参数，详情见 [平台接口认证](../#22-ping-tai-jie-kou-ren-zheng)。
>
> **操作用户**：接口如果要记录操作人，URL上带loginUser参数，详情见 [操作用户](../#51-cao-zuo-yong-hu)。

### 1.3 返回结果示例

```java
[
    {
        "appKey": "streamingut608",
        "normalToken":"xxxx",
        "cname": "streaming单元测试项目",
        "version": "4.2.7",
        //以下字段在【4.5.1版本】中新增
        "logo": "/data/static/files/logo/aaa.png",
        "createTime": 1578901233445,
        "sdkBack": "iOS,Android,H5",
        "status": 1,
        "partitionNum": 3,
        "stream": 0
    }
]
```

#### 1.3.1 出参说明：

| 参数名称         | 类型     | 说明                                            |
| ------------ | ------ | --------------------------------------------- |
| appKey       | String | 项目AppKey                                      |
| normalToken  | String | 项目内接口授权码                                      |
| cname        | String | 项目名称，用于展示                                     |
| version      | String | 项目当前版本信息                                      |
| logo         | String | 项目图标访问路径，默认不显示，只有上传logo后显示                    |
| createTime   | Long   | 十三位时间戳                                        |
| sdkBack      | String | 已回数SDK接入平台(如 Java,JS,Android )，未回数时不显示        |
| status       | int    | 项目状态；1表示正常，2表示已删除，3表示异常不可用，只返回状态值1的项目         |
| partitionNum | int    | 数据存储分区数                                       |
| stream       | int    | 项目数据数据流状态；0表示未启动，1表示启动中，2表示已启动，3表示异常中断，5表示关闭中 |

### 1.4 接口调用示例

```java
curl -H "Content-Type:application/json" -H "xtoken:9CF0444E9DFD9E3D9CAE49B79F939B61" -X GET http://127.0.0.1:4005/uba/manage/enterprise/projects
```

## 2. 获取单个项目详细

### 2.1 接口地址

> 【GET】 /uba/manage/enterprise/projects/{appKey}

### 2.2 请求参数示例

```java
无
```

> **认证参数**：接口必传 xtoken 参数，详情见 [平台接口认证](../#22-ping-tai-jie-kou-ren-zheng)。
>
> **操作用户**：接口如果要记录操作人，URL上带loginUser参数，详情见 [操作用户](../#51-cao-zuo-yong-hu)。

#### 2.2.1 入参说明：

| 参数名称   | 类型     | 必填 | 说明               |
| ------ | ------ | -- | ---------------- |
| appKey | String | Y  | 项目App标识，备注：URL传参 |

### 2.3 返回结果示例

```java
{
    "appKey":"streamingut608",
    "cname":"streaming单元测试项目",
    "version":"4.2.7",
    "logo":"/data/static/files/logo/aaa.png",
    "createTime":1578901233445,
    "sdkBack":"iOS,Android,H5",
    "status":1,
    "partitionNum":3,
    "stream":0
}
```

#### 2.3.1 出参说明：

| 参数名称         | 类型     | 说明                                                  |
| ------------ | ------ | --------------------------------------------------- |
| appKey       | String | 项目AppKey                                            |
| cname        | String | 项目名称，用于展示                                           |
| version      | String | 项目当前版本信息                                            |
| logo         | String | 项目图标访问路径，默认不显示，只有上传logo后显示                          |
| createTime   | Long   | 十三位时间戳                                              |
| sdkBack      | String | 已回数SDK接入平台(如 Java,JS,Android )，未回数时不显示              |
| status       | int    | <p>项目状态；</p><p>1表示正常，2表示已删除，3表示异常不可用，只返回状态值1的项目</p> |
| partitionNum | int    | 数据存储分区数                                             |
| stream       | int    | 项目数据数据流状态；0表示未启动，1表示启动中，2表示已启动，3表示异常中断，5表示关闭中       |

### 2.4 接口调用示例

```java
curl -H "Content-Type:application/json" -H "xtoken:9CF0444E9DFD9E3D9CAE49B79F939B61" -X GET http://127.0.0.1:4005/uba/manage/enterprise/projects/streamingut608
```

## 3. 创建新项目

### 3.1 接口地址

> 【POST】 /uba/manage/enterprise/projects

### 3.2 请求参数示例

```java
{
      "appKey":" streamingut608",
      "name":"测试项目"
}
```

> **认证参数**：接口必传 xtoken 参数，详情见 [平台接口认证](../#22-ping-tai-jie-kou-ren-zheng)。
>
> **操作用户**：接口如果要记录操作人，URL上带loginUser参数，详情见 [操作用户](../#51-cao-zuo-yong-hu)。

#### 3.2.1 入参说明：

| 参数名称   | 类型     | 必填 | 说明                                                      |
| ------ | ------ | -- | ------------------------------------------------------- |
| appKey | String | Y  | <p>新项目的AppKey标识，只接受英文数字组合，不传系统自动生成。</p><p>备注：Body参数</p> |
| name   | String | Y  | 项目名称，只接受英文数字组合。                                         |

### 3.3 返回结果示例

```java
{
    "appKey": "streamingut608",
    "success": 0
}
```

#### 3.3.1 出参说明：

| 参数名称    | 类型      | 说明                                                                                                 |
| ------- | ------- | -------------------------------------------------------------------------------------------------- |
| appKey  | String  | 项目AppKey                                                                                           |
| success | Integer | <p>0表示创建完成，无异常。</p><p>备注：因为项目创建需要调配非常多系统资源，所以该接口为异步操作，项目真正可用状态需要调用【项目详情】接口，其中status 字段表示项目创建情况</p> |

### 3.4 接口调用示例

```java
curl -H "Content-Type:application/json" -H "xtoken:9CF0444E9DFD9E3D9CAE49B79F939B61" -X POST --data '{" appKey ":" streamingut608","name ":"测试项目"}'  http://127.0.0.1:4005/uba/manage/enterprise/projects
```

## 4 开启/关闭数据流

### 4.1 接口地址

> 【POST】 /uba/manage/enterprise/projects/{appKey}/stream

### 4.2 请求参数示例

```java
{
    //数据流状态 true为开启数据流 false为关闭数据流 关闭数据流功能在4.5版本中新增
    "streamSwitch": true
}
```

> **认证参数**：接口必传 xtoken 参数，详情见 平台接口认证。
>
> **操作用户**：接口如果要记录操作人，URL上带loginUser参数，详情见 操作用户。

#### 4.2.1 入参说明：

| 参数名称         | 类型      | 必填 | 说明                                                              | 枚举         |
| ------------ | ------- | -- | --------------------------------------------------------------- | ---------- |
| appKey       | String  | Y  | 新项目的AppKey标识，只接受英文数字组合，不传系统自动生成。备注：URL参数                        |            |
| streamSwitch | Boolean | Y  | <p>数据流状态 true为开启数据流，false为关闭数据流。</p><p>备注：关闭数据流在4.5版本中才会支持。</p> | true/false |

### 4.3 返回结果示例

```java
{
  //0表示操作成功，数据流开启/关闭中
  "success": 0
}
```

#### 4.3.1 出参说明：

| 参数名称    | 类型      | 说明                                                                                     |
| ------- | ------- | -------------------------------------------------------------------------------------- |
| success | Integer | 0表示操作成功，数据流开启/关闭中。备注：因为开启数据流/关闭数据流是异步操作，接口调用只是发起了相关请求，最终的操作结果需要通过streamStatus查看最终启停状态。 |

### 4.4 接口调用示例

```java
curl -H "Content-Type:application/json" -H "xtoken:E1E967DCE07B10839F87195B78E1F5F5" -X POST --data '{
    "streamSwitch": true
}' http://127.0.0.1:4005/uba/manage/enterprise/projects/streamingut608/stream?loginUser=admin@analysys.com.cn
```
