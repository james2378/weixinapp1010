### 介绍
java毕业设计，微信小程序订餐系统
### 3000多套系统，需要联系
抠：3565014707 微：a13424421017

#### 软件架构
##### 整体架构模式
这是一个 多端协同的餐饮管理系统，采用 前后端分离架构，包含以下模块：

微信小程序端（mp-weixin）：面向消费者，提供菜品浏览、下单、评价等功能。

管理后台（ssm04gz3/src/main/webapp/admin）：基于 Vue.js + ElementUI 的后台管理系统，供商家管理菜品、订单、配送等。

后端服务（ssm04gz3）：基于 Spring Boot + MyBatis 的 Java 服务，提供统一 API 和业务逻辑。
##### 分层架构设计
后端分层（ssm04gz3模块）：

Controller层：controller 包（如 CaipinfenleiController）处理 HTTP 请求，返回 JSON 数据。

Service层：service 包（如 CaipinfenleiService）实现核心业务逻辑（如菜品分类管理、订单处理）。

DAO层：dao 包（如 CaipinfenleiDao）通过 MyBatis XML 文件（CaipinfenleiDao.xml）操作数据库。

实体与数据模型：

entity 包定义数据库实体（如 CaipinfenleiEntity 菜品分类实体）；

vo（值对象）和 view（视图模型）用于接口数据传输和复杂查询结果封装。

前端分层（以微信小程序为例）：

视图层：pages 目录定义页面（如 caipinxinxi 菜品详情页），通过 .wxml（模板）和 .wxss（样式）构建界面。

组件层：components 封装可复用组件（如 mescroll-uni 滚动加载组件、w-picker 时间选择器）。

状态管理：通过全局变量或轻量级状态库（如 store.js）管理用户登录状态和购物车数据。
##### 关键技术特性
多端适配：

微信小程序端使用原生组件（如 uni-popup 弹窗）；

管理后台使用 ElementUI 组件库（如表格、表单）。

权限控制：

后端通过 AuthorizationInterceptor 拦截器校验用户 Token 和权限；

前端管理后台通过路由（router-static.js）控制页面访问权限。

第三方服务集成：

BaiduUtil 可能用于地图服务（如配送路线规划）；

支付模块通过 config.properties 配置密钥，支持微信/支付宝支付。
#### 核心功能模块解析
##### 用户端功能（微信小程序）
菜品浏览与下单：

caipinxinxi（菜品信息）：展示菜品详情（图片、价格、描述），支持加入购物车。

shop-cart（购物车）：管理待结算商品，支持数量修改和删除。

pay-confirm（支付确认）：选择配送地址，完成订单支付。

订单与售后：

dingdanxinxi（订单信息）：查看订单状态（待配送、已完成），支持取消订单。

dingdantousu（订单投诉）：提交售后申请，描述问题并上传凭证。

用户互动：

caipinpingjia（菜品评价）：用户对已消费菜品进行评分和文字评价。

chat（在线沟通）：与商家客服实时沟通，解决配送或菜品问题。

##### 管理后台功能（Vue.js）
菜品与分类管理：

caipinfenlei（菜品分类）：定义分类（如热销、主食、饮品），调整展示顺序。

caipinxinxi（菜品管理）：维护菜品信息（名称、价格、库存），上下架控制。

订单与配送：

dingdanxinxi（订单管理）：处理订单配送、打印小票，标记异常订单。

peisongxinxi（配送信息）：管理骑手信息，分配配送任务。

数据统计：

discusscaipinxinxi（菜品评价分析）：统计好评率、高频关键词，优化菜品设计。
##### 后端核心服务
通用业务逻辑：

CommonController 提供通用 CRUD 接口，支持动态 SQL（CaipinfenleiDao.xml）；

MyMetaObjectHandler 实现 MyBatis-Plus 自动填充（如 create_time、update_time）。

订单与支付：

支付模块通过 config.properties 读取密钥，调用第三方支付 API；

订单超时未支付自动取消（通过定时任务实现）。
