# 成员管理

易观方舟企业管理后台支持多个项目多个成员共享，方便企业内部共同参与到数据分析和决策的过程中来。

## 1. 角色-权限

企业平台预置了常用的角色，不同角色对应不同的权限，平台管理员授权时对不同的成员选择不同的角色即可。

| 角色    | 角色描述              | 企业概览 | 成员管理 | 项目管理 | 安全设置 | 进入具体项目         |
| ----- | ----------------- | ---- | ---- | ---- | ---- | -------------- |
| 平台管理员 | 通常赋予企业负责人         | √    | √    | √    | √    | √              |
| 平台运维  | 通常赋予运维人员该角色       | √    |      | √    |      | 在项目中被添加为成员时可进入 |
| 项目管理员 | 通常赋予项目的leader     |      |      |      |      | √              |
| 平台成员  | 通常赋予仅可查看某些项目的普通成员 |      |      |      |      | 在项目中被添加为成员时可进入 |

更多权限明细详见《易观方舟角色-权限对应表》 [https://shimo.im/sheets/6hGxwHhHXXRktTcY/HUvKN](https://shimo.im/sheets/6hGxwHhHXXRktTcY/HUvKN)

## 2. 邀请成员

点击左侧导航栏成员管理，进入成员列表页面，可以看到用户的基本信息，姓名、用户名、邮箱、手机号、加入时间和授权角色。

点击右上角 **添加成员**，输入：成员姓名、用户名、邮箱、初始密码、手机号（选填）、所属部门（选填）和授权角色 即可创建成员帐号。

![ ](https://imguserradar.analysys.cn/fangzhou/img/2018/12/201812181426259399.gif)

添加成功后，被邀请成员就可以使用 **邮箱/手机号/用户名** 和 **初始密码** 进行登录。

## 3. 修改成员

在成员列表页可以查看企业中，有哪些成员以及不同成员的角色，移入某个成员后可以修改其权限、密码，或移除该成员。

![ ](https://imguserradar.analysys.cn/fangzhou/img/2018/12/201812181430409286.png)

### **A. 修改成员**

需要修改用户信息或者权限时，可以点击修改成员按钮，快速修改

![ ](https://imguserradar.analysys.cn/fangzhou/img/2018/12/201812181437381573.png)

### **B. 修改成员密码**

当用户忘记密码时，可以进行重置成员密码

![image](https://imguserradar.analysys.cn/fangzhou/img/2018/08/201808101536015639.png)

### **C. 移除成员**

当添加的成员已离职，或者不再授权时，点击移除成员，移除后将无法访问该企业数据。

{% hint style="info" %}
考虑到数据完整性移除成员并不会将成员从系统中删除。如果未来想恢复某个曾经移除的用户时，可以在用户列表中搜索该用户，并将其状态置为“开启”。
{% endhint %}

![ ](https://imguserradar.analysys.cn/fangzhou/img/2018/12/201812181441586846.png)





{% hint style="info" %}
以上内容没有解答我的问题？[点击我来反馈](https://support.qq.com/products/118522/) 🚀
{% endhint %}
