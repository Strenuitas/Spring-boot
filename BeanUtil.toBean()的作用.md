# BeanUtil.toBean 的行为

### 它会把 源对象（requestParam）里的属性值，按 字段名匹配，拷贝到目标对象（ShortLinkCreateReqDTO）中。

### 只有当 两个类里都有相同字段 时才会赋值。

### 源对象有但目标类没有的字段（比如 originUrls、describes），不会出现在目标对象里。
