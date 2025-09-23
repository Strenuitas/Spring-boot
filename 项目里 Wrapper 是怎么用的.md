### 在 Service 层里，我通过 QueryWrapper 来动态拼接 SQL 条件，然后调用 BaseMapper 提供的 selectList 或 selectMaps 方法执行查询。
### 对于复杂的统计查询，我会考虑直接用 @Select 注解或者 XML 写 SQL，因为 Wrapper 写起来冗长不直观。
