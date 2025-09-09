```text
客户端（浏览器/前端）
         |
         |  GET /api/shortlink/v1/user/{username}
         v
+---------------------+
|  UserController     |  <- 接收请求，调用 Service
+---------------------+
         |
         v
+---------------------+
|  UserServiceImpl    |  <- 业务逻辑层
| - 构建查询条件       |
| - 调用 Mapper 查询   |
| - 将 UserDO 转 DTO  |
+---------------------+
         |
         v
+---------------------+
|  UserMapper         |  <- 数据访问层（MyBatis-Plus）
| - 自动生成 SQL       |
| - SELECT * FROM t_user WHERE username = ? |
+---------------------+
         |
         v
+---------------------+
|  数据库 t_user       |  <- 查询匹配记录，返回 UserDO
+---------------------+
         |
         v
+---------------------+
|  UserServiceImpl    |  <- 转换成 UserRespDTO
+---------------------+
         |
         v
+---------------------+
|  UserController     |  <- 包装成 Result<UserRespDTO>
+---------------------+
         |
         v
客户端收到 JSON:
{
  "code": "0",
  "message": "success",
  "data": {
    "username": "wangba",
    "email": "xxx@test.com",
    "phone": "123456789"
  }
}
