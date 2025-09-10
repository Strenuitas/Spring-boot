```mermaid
flowchart TD
    A[客户端请求<br>GET /api/shortlink/v1/user/has-username?username=zhangsan] --> B[UserController<br>@GetMapping<br>@RequestParam<br>调用 userService.hasUsername()]
    B --> C[UserService<br>接口类型 userService<br>调用 UserServiceImpl 实现]
    C --> D[UserServiceImpl<br>实现业务逻辑<br>构造 LambdaQueryWrapper<br>调用 baseMapper.selectOne()]
    D --> E[UserMapper<br>继承 BaseMapper<UserDO><br>执行 SQL 查询<br>SELECT * FROM user WHERE username = ?]
    E --> F[数据库 (DB)<br>user 表<br>查找 username=zhangsan]
    F --> G[返回结果<br>true/false → Controller → 客户端]
