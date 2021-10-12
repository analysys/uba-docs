# 脚本工具

对于私有化部署的客户，有的情况下可能会需要对项目进行一些更高级的操作，我们提供了一些脚本。

它们位于：

```bash
/opt/soft/streaming/bin/
```

具体如下：

| 功能描述                        | 脚本名称                         | 参数说明                                                                                                                                                                                                                                               |
| --------------------------- | ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **创建项目**                    | create_project.sh            | <p><strong>enterpriseId</strong> 企业id 是一个固定值 1</p><p><strong>appKey</strong> 创建项目的appKey</p><p><strong>project_cname</strong> 创建项目的中文名称</p>                                                                                                        |
| **删除项目**                    | drop_project.sh              | **appKey** 要删除的项目的appKey                                                                                                                                                                                                                           |
| **启动一个项目的实时流**              | start_streaming.sh           | **appKey** 要启动实时流的项目的appKey                                                                                                                                                                                                                        |
| **停止一个项目的实时流**              | stop_streaming.sh            | **appKey** 要停止实时流的项目的appKey                                                                                                                                                                                                                        |
| **停止所有项目的实时流**              | stop_all_streaming.sh        |                                                                                                                                                                                                                                                    |
| **重置方舟 admin 用户的密码为111111** | reset_manager_password.sh    |                                                                                                                                                                                                                                                    |
| **修改已经存在的数据类型**             | update_datatype_scheduler.sh | <p><strong>appkey</strong> 要操作的项目的 appKey </p><p><strong>table</strong> 表名 [event|profile] </p><p><strong>column</strong> 列名 </p><p><strong>datatype</strong> 目标数据类型</p><p><strong>startdate</strong> 起始日期</p><p><strong>enddate</strong> 截止日期</p> |



{% hint style="info" %}
以上内容没有解答我的问题？[点击我进入方舟论坛去反馈](https://www.analysysdata.com/forum/index) 🚀
{% endhint %}
