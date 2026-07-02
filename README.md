# 仿QQ即时通讯系统 — 课程设计团队博客

---

## 一、项目简介

本项目是一个基于 **Java Swing + MySQL + TCP Socket** 的桌面即时通讯软件，采用 C/S 架构，实现了用户注册登录、好友管理、群聊、私聊、消息撤回、文件/图片传输等核心即时通讯功能。界面风格仿照 QQ，设计美观现代，交互流畅。  
系统支持多用户同时在线，服务端通过多线程处理每个客户端连接，使用自定义消息协议进行高效通信，所有聊天记录和用户数据持久化存储于 MySQL 数据库。

---

## 二、项目采用技术

| 技术分类 | 具体实现 |
|----------|----------|
| **编程语言** | Java (JDK 11+) |
| **客户端 UI** | Java Swing（自绘组件：气泡、列表项、滚动条等） |
| **网络通信** | TCP Socket + 自定义序列化协议（ObjectStream） |
| **数据库** | MySQL 8.0 |
| **并发处理** | 多线程（线程池、心跳线程、消息接收线程） |
| **设计模式** | 分层架构：dao（数据访问层）、service（业务逻辑层）、view（界面层） |
| **版本控制** | Git + GitHub，使用 Issue 进行任务管理 |

### 详细技术使用表

| 技术类别 | 是否使用 | 具体项目 |
|----------|----------|----------|
| 文件/数据库 | ✓ | MySQL 8.0（用户、好友、消息持久化） |
| GUI | ✓ | Java Swing（自定义大量组件） |
| 网络 | ✓ | TCP Socket + 自定义序列化协议 |
| 多线程 | ✓ | 服务端线程池、客户端心跳线程、消息接收线程 |
| DAO/MVC | ✓ | 分层：dao、service、view |
| Git | ✓ | GitHub 进行版本控制和发布 |
| Issue | ✓ | 使用 GitHub Issues 分配任务、跟踪 bug |
| 配置文件 | ✓ | database.properties |
| 日志文件 | ✓ | 控制台输出及异常打印 |
| 容错处理 | ✓ | 网络断开重连、文件发送失败提示等 |
| 界面美观 | ✓ | 仿QQ风格，自绘气泡、阴影、未读红点 |

---

## 三、功能需求分析

### 1. 用户管理
- 用户注册（用户名、密码），密码加密存储
- 用户登录/登出，登录后状态自动更新为“在线”
- 在线状态实时同步（心跳检测，30秒间隔）
- 个人资料查看与修改（支持修改用户名和密码，弹窗交互）

### 2. 好友管理
- 加载好友列表（置顶优先排序）
- 通过输入用户 ID 直接添加好友
- 删除好友（带确认提示）
- 好友置顶/取消置顶（右键菜单操作）
- 好友搜索（按用户名实时过滤）
- 好友在线状态实时显示（绿点/灰点）

### 3. 群聊管理
- 创建群组（输入群名称）
- 通过输入群 ID 加入现有群组
- 查看群成员列表（弹出窗口显示昵称和 ID）
- 查看群 ID 并一键复制到剪贴板
- 群聊消息广播，所有成员均能收到消息

### 4. 即时通讯核心
- **私聊消息**：消息气泡左右对齐（自己发送的消息靠右，对方靠左）
- **群聊消息**：群内每位成员都能看到消息，并显示发送者昵称
- **消息撤回**：发送方右键消息选择“撤回”，服务端标记消息为已删除，并通知接收方同步更新界面
- **文本消息**：自动换行，圆角矩形气泡，带轻微阴影
- **文件/图片传输**：发送方通过工具栏选择文件或图片，服务端接收后存储到本地，并将文件路径转发给接收方；接收方聊天区显示文件卡片（图标、文件名、大小），点击“下载”按钮可保存到本地

### 5. 聊天记录持久化
- 私聊与群聊消息全部存入 MySQL 数据库
- 每次打开聊天窗口自动加载最近 100 条历史消息
- 消息类型区分：文本、图片、文件

### 6. 界面交互细节
- 好友/群聊列表项：鼠标悬停背景变色，点击选中高亮
- 右键菜单功能：好友置顶、删除好友；群聊查看成员、复制群 ID
- 自定义滚动条（细条、圆角、无箭头）
- 个人主页弹窗：顶部显示头像、昵称、ID，下方提供修改昵称和密码的按钮

---

## 四、项目亮点

1. **仿 QQ 风格 UI**  
   自绘圆角聊天气泡（可选阴影、无尖角），好友列表展示未读红点，整体界面现代简洁，交互自然。

2. **完整的文件传输功能**  
   支持任意格式文件传输，图片自动识别并显示 🖼 图标；服务端存储文件并转发，接收方点击“下载”即可保存到本地任意位置，体验接近 QQ。

3. **稳定高效的网络通信**  
   基于 TCP 的自定义消息协议，服务端使用线程池管理多客户端，配合心跳机制保持连接；消息实时收发，撤回操作同步刷新，数据可靠。

4. **良好的分层架构与代码规范**  
   采用 dao / service / view 三层架构，模块间低耦合，便于维护和扩展。代码注释充分，关键逻辑都有说明。

5. **丰富的异常处理**  
   网络断开、文件发送失败、数据库操作异常等均有友好的提示或日志记录，系统健壮性较好。

---

## 五、系统演示截图

### 1.登录界面

<img width="300" alt="QQ20260702-161308" src="https://raw.githubusercontent.com/syk-qlu/syk-qlu.github.io/main/images/QQ20260702-161308.png" />

 
### 2.主聊天界面（私聊）

<img width="300" alt="QQ20260702-161407" src="https://raw.githubusercontent.com/syk-qlu/syk-qlu.github.io/main/images/QQ20260702-161407.png" />


### 3.文件传输卡片

<img width="300"  alt="QQ20260702-161538" src="https://raw.githubusercontent.com/syk-qlu/syk-qlu.github.io/main/images/QQ20260702-161538.png" />


### 4.个人主页修改资料

<img width="300" alt="QQ20260702-161608" src="https://raw.githubusercontent.com/syk-qlu/syk-qlu.github.io/main/images/QQ20260702-161608.png" />


### 5.群成员查看及复制 ID
<img width="300" alt="QQ20260702-161648" src="https://raw.githubusercontent.com/syk-qlu/syk-qlu.github.io/main/images/QQ20260702-161648.png" />

<img width="300" alt="QQ20260702-161745" src="https://raw.githubusercontent.com/syk-qlu/syk-qlu.github.io/main/images/QQ20260702-161745.png" />


### 6.消息发送效果

<img width="300"  alt="QQ20260702-161811" src="https://raw.githubusercontent.com/syk-qlu/syk-qlu.github.io/main/images/QQ20260702-161811.png" />


---

## 六、团队成员分工及工作量

| 成员 | 角色 | 负责模块 | 核心源代码文件 | 代码行数 |
|------|------|----------|----------------|----------|
| **孙元康** (组长) | 服务端 & 通信 & 业务逻辑 | 1. 服务端通信框架搭建<br>2. 客户端网络通信<br>3. 消息协议定义及序列化<br>4. 私聊/群聊/文件消息处理（含数据库存储）<br>5. 数据库表设计<br>6. 消息显示及发送逻辑（部分UI） | ChatServer.java, ClientHandler.java, ChatClient.java, ChatMessage.java, MessageProtocol.java, ChatService.java (部分), MessageBubblePanel.java, ChatBubble.java, ChatFrame.java (消息发送/显示) | 约 1550 |
| **王宇轩** | 客户端 UI 及界面交互 | 1. 主界面框架布局<br>2. 好友列表面板及好友Item组件<br>3. 群组列表面板及群Item组件<br>4. 登录及注册界面<br>5. 文件/图片发送对话框<br>6. 自定义滚动条及平滑滚动 <br>7.主页面按键交互（左侧导航栏）| ChatFrame.java (整体布局), ContactListPane.java, ContactItem.java, GroupListPane.java, GroupItem.java, LoginFrame.java, FileTransferDialog.java, ScrollBarUI.java, SmoothScroll.java | 约 1300 |
| **王常兴** | 数据层 & 工具类 | 1. 实体模型类设计<br>2. 数据库连接管理<br>3. 用户、好友、群组、消息的 DAO 实现<br>4. 图片头像工具类、文件工具类、日期工具类封装<br>5. 界面常量配置 | User.java, Group.java, Message.java, FriendRequest.java, ChatMessage.java (部分), DBConnection.java, UserDAO.java, FriendshipDAO.java, GroupDAO.java, MessageDAO.java, ImageUtil.java, FileUtil.java, DateUtil.java, Constants.java | 约 1500 |


---

## 七、项目 Git 地址与提交记录

- **GitHub 仓库**：[https://github.com/team-chat-app/qq-chat](https://github.com/team-chat-app/qq-chat)

### Git 提交记录截图

#### 孙元康

<img width="300" alt="QQ20260702-161608" src="https://raw.githubusercontent.com/syk-qlu/syk-qlu.github.io/refs/heads/main/images/6282a856-0c60-4aa8-a83a-84f8091264ee.png" />

#### 王宇轩

<img width="300" alt="QQ20260702-161608" src="https://raw.githubusercontent.com/syk-qlu/syk-qlu.github.io/refs/heads/main/images/0f3021a7-de33-4bb6-8210-e19e7691d749.png" />

#### 王常兴

<img width="300" alt="QQ20260702-161608" src="https://raw.githubusercontent.com/syk-qlu/syk-qlu.github.io/refs/heads/main/images/7f534ff2-5169-4aa5-860a-16db319ff386.png" />

---

## 八、课程设计感受

**感受**：  
通过本次课程设计，我们小组真正掌握了一个 C/S 架构即时通讯系统的完整开发流程。从数据库设计、服务端通信搭建，到客户端界面绘制和消息逻辑实现，每一环节都充满挑战。特别是文件传输和消息撤回的同步问题，让我们深刻理解了网络编程中数据一致性的重要性。Git 协作和 Issue 管理也锻炼了我们的团队开发能力。


---

*谢谢！*
