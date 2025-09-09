```text
客户端（浏览器/前端） 
         |
         |  GET /api/shortlink/v1/user/{username}
         v
-------------------------------------------------
|               UserController                 |
|-----------------------------------------------|
| @RestController                               |
| public Result<UserRespDTO> getUserByUsername()|
|   -> 调用 userService.getUserByUsername()    |
-------------------------------------------------
         |
         v
-------------------------------------------------
|               UserServiceImpl                |
|-----------------------------------------------|
| extends ServiceImpl<UserMapper, UserDO>      |
| @Override                                     |
| public UserRespDTO getUserByUsername()       |
|   -> 构建 LambdaQueryWrapper                 |
|   -> 调用 baseMapper.selectOne(queryWrapper) |
|   -> 将 UserDO 转成 UserRespDTO (BeanUtils) |
-------------------------------------------------
         |
         v
-------------------------------------------------
|                  UserMapper                  |
|-----------------------------------------------|
| MyBatis-Plus 自动生成 SQL                    |
| SELECT * FROM t_user WHERE username = ?      |
-------------------------------------------------
         |
         v
-------------------------------------------------
|                    数据库                     |
|-----------------------------------------------|
| 表 t_user 查询匹配 username 的记录           |
| 返回 UserDO 对象                              |
-------------------------------------------------
         |
         v
-------------------------------------------------
| UserServiceImpl                                |
| 将 UserDO 转成 UserRespDTO                     |
-------------------------------------------------
         |
         v
-------------------------------------------------
| UserController                                |
| 包装成 Result<UserRespDTO>                    |
| 返回给前端                                    |
-------------------------------------------------
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
