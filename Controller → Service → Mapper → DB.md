客户端请求：
GET /api/shortlink/v1/user/has-username?username=zhangsan
        │
        ▼
┌───────────────────────────┐
│      UserController       │
│ - @GetMapping 接收请求     │
│ - @RequestParam("username")│
│ - 调用 userService.hasUsername(username) │
└───────────▲───────────────┘
            │
            ▼
┌───────────────────────────┐
│       UserService         │
│ (接口类型变量 userService)│
│ - hasUsername(username)   │
│ - 调用 UserServiceImpl 实现│
└───────────▲───────────────┘
            │
            ▼
┌───────────────────────────┐
│     UserServiceImpl       │
│ - 实现业务逻辑            │
│ - 构造 LambdaQueryWrapper │
│ - 调用 baseMapper.selectOne(queryWrapper) │
└───────────▲───────────────┘
            │
            ▼
┌───────────────────────────┐
│        UserMapper         │
│ - 继承 BaseMapper<UserDO> │
│ - 执行 SQL 查询            │
│   SELECT * FROM user       │
│   WHERE username = ?       │
└───────────▲───────────────┘
            │
            ▼
┌───────────────────────────┐
│         数据库 (DB)       │
│ - user 表                 │
│ - 查找 username=zhangsan   │
└───────────────────────────┘
            │
            ▼
返回结果：
数据库 → Mapper → UserServiceImpl → UserService → Controller → 客户端
- true/false（用户名是否存在）
