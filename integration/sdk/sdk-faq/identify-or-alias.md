# identify与alias的区别

  首先需要了解在目前提供的移动端SDK中，都会有SDK本身生成一个匿名的ID，用来标识设备。

* `identify`与`alias`的作用

`identify`：修改为自行业务需求的匿名ID，不使用由系统生成的\
`alias`：作用是向服务器发送一条绑定信息，告知服务端你需要绑定的信息，对前后同一用户行为进行关联。

* `identify`与`alias`的场景

`identify`：需要使用自身业务系统的标识，优先调用如App可以在初始化之前、Web方面需要在初始化后立即调用\
`alias`：可以获取到用户是登录状态的地方，或注册完毕后都可以调用
