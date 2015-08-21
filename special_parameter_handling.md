# 特殊参数处理

正如上面所看到的那样，在您的查询中处理参数，您只需定义方法参数。除了基本的还要识别某些特别的类型像Pageable和Sort这些在你的查询中提供动态的分页和排序。

示例9。使用Pageable,Slice和Sort在查询方法中

```java
         Page<User> findByLastname(String lastname, Pageable pageable);
         
         Slice<User> findByLastname(String lastname, Pageable pageable);
         
         List<User> findByLastname(String lastname, Sort sort);
         
         List<User> findByLastname(String lastname, Pageable pageable);
```

第一个方法允许在你的查询方法的静态定义查询中通过一个org.springframework.data.domain.Pageable实例来动态的添加分页。分页类知道元素的总数和可用页数。它通过基础库来触发一个统计查询计算所有的总数。由于这个查询可能对store消耗巨大，可以使用Slice来替代。Slice仅仅知道是否有下一个Slice可用，这对查询大数据已经足够了。

排序选项和分页的处理方式一样。如果你需要排序，简单的添加一个org.springframework.data.domain.Sort参数到你的方法即可。也正如你所见，简单的返回一个列表也是可以的，在这种情况下，生产的分页实例所需的附加元数据将不会被创建(这也意味着额外的计数查询可能需要但不一定被公布)。

> 要找到在你的查询中有多少页，你需要触发一个额外的计数查询。按照默认来说这个查询可以从你实际触发查询中衍生出来