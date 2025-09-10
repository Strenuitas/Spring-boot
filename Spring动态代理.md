# Java 动态代理笔记

## 1. 什么是代理模式？
- **代理模式**：给某个对象提供一个代理对象，由代理对象来控制对原对象的访问。
- 分类：
  - **静态代理**：在编译时就确定代理类（需要手写代理类）。
  - **动态代理**：在运行时动态生成代理类（不用提前写死代理类）。

---

## 2. 为什么需要动态代理？
- 如果我们有很多接口，每个接口都需要加日志/权限/事务等功能：
  - 静态代理需要为每个接口写一个代理类，代码重复、维护困难。
  - 动态代理可以在运行时 **自动生成代理类**，在调用目标方法前后插入增强逻辑。

---

## 3. 动态代理的实现方式
### 3.1 JDK 动态代理
- 使用 Java 自带的 `java.lang.reflect.Proxy` 和 `InvocationHandler`。
- 要求：**被代理的类必须实现接口**。

#### 核心类
- **`Proxy.newProxyInstance`**：生成代理对象。
- **`InvocationHandler`**：定义代理逻辑（调用目标方法前后做什么）。

#### 示例代码
```java
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

// 1. 定义接口
interface UserService {
    void addUser(String name);
}

// 2. 实现类
class UserServiceImpl implements UserService {
    @Override
    public void addUser(String name) {
        System.out.println("添加用户：" + name);
    }
}

// 3. 动态代理处理器
class LogInvocationHandler implements InvocationHandler {
    private final Object target;

    public LogInvocationHandler(Object target) {
        this.target = target;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("[日志] 调用方法: " + method.getName());
        Object result = method.invoke(target, args); // 调用目标对象方法
        System.out.println("[日志] 方法结束: " + method.getName());
        return result;
    }
}

// 4. 使用动态代理
public class DynamicProxyDemo {
    public static void main(String[] args) {
        UserService target = new UserServiceImpl();

        UserService proxy = (UserService) Proxy.newProxyInstance(
                target.getClass().getClassLoader(),
                target.getClass().getInterfaces(),
                new LogInvocationHandler(target)
        );

        proxy.addUser("张三");
    }
}
