# 特殊参数处理

正如上面所看到的那样，在您的查询中处理参数，您只需定义方法参数。除了基本的还要识别某些特别的类型像Pageable和Sort这些在你的查询中提供动态的分页和排序。

示例9。使用Pageable,Slice和Sort在查询方法中

```java
         Page<User> findByLastname(String lastname, Pageable pageable);
         
         Slice<User> findByLastname(String lastname, Pageable pageable);
         
         List<User> findByLastname(String lastname, Sort sort);
         
         List<User> findByLastname(String lastname, Pageable pageable);
```

第一个方法允许在你的查询方法的静态定义查询中通过一个org.springframework.data.domain.Pageable实例来动态的添加分页。分页类知道元素的总数和可用页数。