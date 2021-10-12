# 成员管理

## 1. 注册企业用户

方舟企业管理后台支持多个项目成员共享，在添加项目成员前需要先注册用户。

### 1.1 接口地址

> 【POST】 /uba/manage/enterprise/accounts

### 1.2 请求参数示例

```java
{
    //【必填】邮箱地址
    "email": "api@analysys.com.cn",
    //用户名
    "userName": "api",
    //真实姓名
    "name": "接口用户",
    // 密码 【4.5.1之前的版本密码为必填，4.5.1之后为不必填】
    "password": "123456",
    // 手机号码
    "phone": "1380000000",
    //用户所属部门
    "department": "技术部"
}
```

> **角色**：通过接口添加的用户角色默认为平台成员。
>
> **认证参数**：接口必传 xtoken 参数，详情见 [平台接口认证](../#22-ping-tai-jie-kou-ren-zheng)。
>
> **操作用户**：接口如果要记录操作人，URL上带loginUser参数，详情见 [操作用户](../#51-cao-zuo-yong-hu)。

#### 1.2.1 入参说明：

| 参数名称       | 类型     | 必填 | 说明                   |
| ---------- | ------ | -- | -------------------- |
| email      | String | Y  | 邮箱 不能重复 可用于登录        |
| userName   | String | N  | 用户名：不能重复 可用于登录       |
| name       | String | N  | 真实姓名：常用于展示           |
| password   | String | N  | 登录密码【 4.5.1版本修改为不必填】 |
| phone      | String | N  | 手机号码：不能重复 可用于登录      |
| department | String | N  | 用户所属部门               |

### 1.3 返回结果示例

```java
{
    //用户新增成功会返回方舟产品中对应的用户ID
    "userId":1,
    //邮箱地址
    "email":"api@analysys.com.cn"
}
```

### 1.4 接口调用示例

```java
curl -H "Content-Type:application/json" -H "xtoken:9CF0444E9DFD9E3D9CAE49B79F939B61" -X POST --data '{
    "email": "api@analysys.com.cn",
    "userName": "api",
    "name": "接口用户",
    "password": "123456",
    "phone": "1380000000",
    "department": "技术部"
}' http://127.0.0.1:4005/uba/manage/enterprise/accounts?loginUser=admin@analysys.com.cn
```

## 2. 禁用/启用企业用户

禁用企业用户不会将用户记录删除，只会修改为不可用，禁用只会的帳号将不能登录方舟系统，如果需要继续使用，需要调用接口恢复用户状态。

### 2.1 接口地址

> 【POST】 /uba/manage/ enterprise/accounts/activation

### 2.2 请求参数示例

```java
{
    //【必填】状态：false为禁用 true为启用
    "activation": false
}
```

> **认证参数**：接口必传 xtoken 参数，详情见 [平台接口认证](../#22-ping-tai-jie-kou-ren-zheng)。
>
> **操作用户**：接口如果要记录操作人，URL上带loginUser参数，详情见 [操作用户](../#51-cao-zuo-yong-hu)。

#### 2.2.1 入参说明：

| 参数名称       | 类型      | 必填 | 说明                         | 枚举                      |
| ---------- | ------- | -- | -------------------------- | ----------------------- |
| email      | String  | Y  | 要禁用/启用的用户邮箱，备注：URL传参       |                         |
| activation | Boolean | Y  | false为禁用，true为启用。备注：Body参数 | <p>true</p><p>false</p> |

### 2.3 返回结果示例

```java
{
    //0 表示返回成功
    "success":0
}
```

### 2.4 接口调用示例

```java
curl -H "Content-Type:application/json" -H "xtoken:9CF0444E9DFD9E3D9CAE49B79F939B61" -X POST --data '{
    "activation": false
}' 'http://127.0.0.1:4005/uba/manage/enterprise/accounts/activation?loginUser=admin@analysys.com.cn&email=api@analysys.com.cn'
```
