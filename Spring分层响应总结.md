### 8️⃣ 总结

**Controller**  
- 处理请求/响应  
- 参数解析  
- 调用 Service 层方法  

**Service + Impl**  
- 核心业务逻辑  
- Service 是接口，Impl 实现具体逻辑  

**Mapper**  
- 数据库操作  
- 封装 SQL 查询  

**数据库 (DB)**  
- 存储实体数据  

**依赖注入 & 多态**  
- Controller 持有接口 `UserService`  
- Spring IoC 自动注入 `UserServiceImpl` 实例  
- 调用方法最终执行 Impl 的具体逻辑
