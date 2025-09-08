# Spring MVC 工作流程（面试常问）

## 1. 请求发起
用户发起请求：
- 浏览器输入 URL
- 前端 AJAX 调用

## 2. 前端控制器 DispatcherServlet
- 所有请求先到 `DispatcherServlet`
- 核心作用：统一接收和分发请求

## 3. HandlerMapping 查找处理器
- `DispatcherServlet` 根据请求 URL，查找对应的 Controller 方法
- 通过 `HandlerMapping` 实现 URL → Controller 方法的映射

## 4. 调用 Controller 执行业务逻辑
- Controller 执行具体业务逻辑
- 返回结果：
  - **对象**（如 POJO）
  - **视图名**（String）

## 5. 结果处理
### 5.1 返回对象
- 交给 `HttpMessageConverter` 转为 JSON 或 XML
- 写入 HTTP 响应体，返回给前端

### 5.2 返回视图名
- 交给 `ViewResolver` 解析视图名
- 找到具体页面模板（如 Thymeleaf）
- 渲染页面，返回给客户端

## 6. 响应返回
- 最终结果返回给客户端：
  - 前端页面
  - JSON / XML 数据
