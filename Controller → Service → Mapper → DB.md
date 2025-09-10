```mermaid
flowchart TD
    A[客户端请求<br>GET /api/shortlink/v1/user/has-username?username=zhangsan] --> B[UserController<br>@GetMapping 接收请求<br>@RequestParam("username")<br>调用 userService.hasUsername(username)]
    B --> C[UserService<br>接口类型变量 userService<br>调用 UserServiceImpl 实现]
    C --> D[UserServiceImpl<br>实现业务逻辑<br>构造 LambdaQueryWrapper<br>调用 baseMapper.selectOne(queryWrapper)]
    D --> E[UserMapper<br>继承 BaseMapper<UserDO><br>执行 SQL 查询<br>SELECT * FROM user WHERE username = ?]
    E --> F[数据库 (DB)<br>user 表<br>查找 username=zhangsan]
    F --> G[返回结果<br>数据库 → Mapper → UserServiceImpl → UserService → Controller → 客户端<br>true/false（用户名是否存在）]
