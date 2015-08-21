# 限制查询

查询方法的结果可以通过关键字first或者top来限制,它们可以交替使用。在top/firest后添加数字来表示返回最大的结果数。如果没有数字，则默认假定1作为结果大小。

示例10。用Top和First查询限制结果大小

```java
     User findFirstByOrderByLastnameAsc();

     User findTopByOrderByAgeDesc();

     Page<User> queryFirst10ByLastname(String lastname, Pageable pageable);

     Slice<User> findTop3ByLastname(String lastname, Pageable pageable);

     List<User> findFirst10ByLastname(String lastname, Sort sort);

     List<User> findTop10ByLastname(String lastname, Pageable pageable);
```

限制表达式也支持Distinct关键字。对于限制查询的结果集定义到一个实例中包装这个结果到一个Optional中也是被支持的。

如果分页或者切片被应用到一个限制查询分页(计算多少页可用)则它也能应用于限制结果。

> 要注意结合通过Sort参数动态排序的限制结果容许表达查询的方法为“K”最小的，以及“K”最大的元素。