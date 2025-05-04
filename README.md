# 苍穹外卖系统

## 项目介绍

苍穹外卖系统是一个基于 Spring Boot 的餐饮外卖管理平台，包含商家后台管理系统和用户前台点餐系统。该系统实现了餐厅管理、商品管理、订单管理、用户管理等核心功能，旨在提供完整的餐厅外卖解决方案。

## 系统特点

- **前后端分离**：采用前后端分离的架构，提高开发效率和系统可维护性
- **微信小程序**：用户端使用微信小程序，提供良好的移动端用户体验
- **安全认证**：基于 JWT 的身份认证，保障系统安全
- **数据缓存**：使用 Redis 缓存热点数据，提高系统性能
- **实时通知**：WebSocket 实现订单状态实时通知
- **第三方集成**：集成微信支付、阿里云 OSS 等第三方服务

## 技术栈

- **后端框架**：Spring Boot 2.7.3
- **ORM 框架**：MyBatis
- **数据库**：MySQL
- **缓存**：Redis
- **接口文档**：Knife4j (基于 Swagger)
- **日志框架**：Slf4j + Logback
- **支付集成**：微信支付
- **对象存储**：阿里云 OSS
- **实时通信**：WebSocket

## 项目结构

项目采用 Maven 多模块架构，主要包含以下模块：

```
sky-take-out
├── sky-common    -- 公共模块，包含工具类、常量、异常处理等
│   ├── com.sky.context      -- 上下文管理
│   ├── com.sky.exception    -- 自定义异常
│   ├── com.sky.constant     -- 常量定义
│   ├── com.sky.enumeration  -- 枚举类
│   ├── com.sky.properties   -- 配置属性
│   ├── com.sky.json         -- JSON处理
│   ├── com.sky.result       -- 统一返回结果
│   └── com.sky.utils        -- 工具类
├── sky-pojo      -- 实体类模块，包含DTO、VO、实体类等
│   ├── com.sky.entity       -- 实体类
│   ├── com.sky.dto          -- 数据传输对象
│   └── com.sky.vo           -- 视图对象
└── sky-server    -- 核心业务模块，包含控制器、服务、数据访问层等
    ├── com.sky.controller   -- 控制器层
    │   ├── admin            -- 管理端控制器
    │   └── user             -- 用户端控制器
    ├── com.sky.service      -- 业务逻辑层
    ├── com.sky.mapper       -- 数据访问层
    ├── com.sky.aspect       -- AOP切面
    ├── com.sky.task         -- 定时任务
    ├── com.sky.websocket    -- WebSocket服务
    └── com.sky.config       -- 配置类
```

## 核心功能

### 管理端功能

- **员工管理**：员工登录、退出、添加、修改、列表查询等
- **分类管理**：菜品分类、套餐分类的新增、修改、删除、列表查询等
- **菜品管理**：菜品的新增、修改、删除、启停售、列表查询等
- **套餐管理**：套餐的新增、修改、删除、启停售、列表查询等
- **订单管理**：订单的接单、拒单、派送、完成、取消、列表查询等
- **数据统计**：各类营业数据的统计和查询
- **店铺设置**：店铺营业状态的设置

### 用户端功能

- **用户登录**：微信登录
- **商品浏览**：分类展示、菜品展示、套餐展示等
- **购物车**：添加商品、删除商品、清空购物车等
- **订单管理**：创建订单、支付订单、取消订单、查询订单等
- **地址管理**：地址的新增、修改、删除、列表查询等
- **个人中心**：个人信息查询、修改

## 环境要求

- JDK 1.8+
- Maven 3.6+
- MySQL 5.7+
- Redis 5.0+

## 快速开始

### 1. 克隆项目

```bash
git clone https://github.com/yourusername/sky-take-out.git
```

### 2. 初始化数据库

使用项目中的 SQL 脚本创建数据库和表结构

### 3. 配置应用

项目使用模板配置文件来保护敏感信息。请按照以下步骤配置：

1. 在`sky-server/src/main/resources`目录下找到`application-dev.template.yml`文件
2. 复制该文件并重命名为`application-dev.yml`
3. 根据您的实际环境修改`application-dev.yml`中的配置参数（数据库连接、Redis 连接、阿里云 OSS 等信息）
4. 此配置文件已被添加到`.gitignore`中，不会被提交到版本控制系统

### 4. 编译打包

```bash
mvn clean package -DskipTests
```

### 5. 启动应用

```bash
java -jar sky-server/target/sky-server.jar
```

## 接口文档

启动应用后，访问以下地址查看接口文档：

- 管理端接口文档：http://localhost:8080/doc.html#/admin
- 用户端接口文档：http://localhost:8080/doc.html#/user

## 部署说明

项目支持多环境部署，通过切换`application.yml`中的 profile 来指定环境：

```yaml
spring:
  profiles:
    active: dev # 开发环境
    # active: prod  # 生产环境
    # active: test  # 测试环境
```

## 项目安全

- 敏感配置信息统一配置在非版本控制的环境变量或配置文件中
- 所有 API 接口均使用 JWT 进行身份验证
- 密码等敏感信息使用加密存储
- 接口权限控制，防止未授权访问

## 注意事项

- 生产环境部署前请修改 JWT 密钥
- 请确保微信支付、阿里云 OSS 等第三方服务的配置正确
- 项目中的敏感信息配置文件已在.gitignore 中排除，请妥善保管
- 定期备份数据库，防止数据丢失
