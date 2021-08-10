# ChromeExt2Go
#### Chrome插件自动化群控系统框架, 抽象常用的Dom事件, 通过Chrome插件实现网页自动化操作, 可用于爬虫, 测试等等.

### 应用组成:

- Chrome插件(已经打包好的crx文件), 按照在浏览器上后负责接受来自控制系统发送来的指令, 根据指令控制浏览器进行相关的操作与行为, 并返回响应数据.

- 后端服务程序, 负责监听插件客户端的注册上线, 状态变化. 创建映射实例, 自动化任务的接收, 存储, 分发等.

### 数据传输:

- Chrome插件与后端服务: WebSocket, 任务的每个步骤都将被序列化为JSON数据发送给插件部分解析执行

- 任务发起者与后端服务: HTTP, 在视图中接收参数, 创建任务实例并将添加到任务池, 则完成一次任务的添加


### 优点:

- 使用Chrome插件直接在标准的浏览器上通过Chrome插件API和Dom事件执行自动化程序, 超高的真人模拟;
- 分布式并发执行, 支持同时多个Chrome插件客户端在线一起参与任务执行, 任务与单个tab页绑定, 在一个浏览器上可同时打开N个tab执行任务;
- 可以根据参数指定使用特定的Chrome的插件客户端执行任务, 如果没有合适的客户端任务将存留, 直到有合适的客户端上线;
- 如果任务执行中途, 插件客户端异常下线, 则会将任务自动重置并添加回任务池, 等待调度给其它可以执行任务的插件客户端;

### 缺点:

- 单个任务的执行效率相较于传统的爬虫脚本效率更低
- 要实现高质量的分布式并发执行, 需要在多台PC上部署插件客户端, 成本相对较高

### 使用场景:

- 替代通过ChromeDriver + Selenium实现的自动化项目,在某些数据爬取上, selenium也可能很快被识别为爬虫程序
- 对真人模拟仿真度有极高要求的爬虫项目或测试项目
- 为了账号安全, 不能将账号密码暴露给开发团队或者不太适宜使用传统爬虫方式的项目(比如亚马逊店铺后台数据抓取)
- 有大量闲置电脑, 想要搭建一个扩展性与兼容性高的爬虫集群系统.  
