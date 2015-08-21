# 创建查询

基础Spring Data repository内置的查询生成器机制对于创建实体仓库的约束查询是有用的，它会从方法名中去掉find...By,read...By,query...By,count...By和get...By这些前缀并解析剩下的内容.这些前缀还能包含更多的表达式例如Distinct,设置一个distinct标志并在查询中创建它，然后第一个By的动作就像一个分隔符来表明查询实际标准的开始。最基本的方式你可以在实体属性中定义表达式并用AND和OR连接它们。

```java
     public interface PersonRepository extends Repository<user,Long>{
         List<Person> findByEmailAddressAndLastname(EmailAddress emailAddress, String lastname);
         
         //Enables the distinct flag for the query
         List<Person> findDistinctPeopleByLastnameOrFirstname(String lastname,String firstname);
         
         List<Person> findPeopleDistinctByLastnameOrFirstname(String lastname, String firstname);
         
         // Enabling ignoring case for an individual property
         List<Person> findByLastnameIgnoreCase(String lastname);
         // Enabling ignoring case for all suitable properties
         List<Person> findByLastnameAndFirstnameAllIgnoreCase(String lastname, String firstname);

         // Enabling static ORDER BY for a query
         List<Person> findByLastnameOrderByFirstnameAsc(String lastname);
         List<Person> findByLastnameOrderByFirstnameDesc(String lastname);
     }
```

解析方法实际的结果依赖于你创建查询的持久存储。然后这里还算是有一些需要注意的事情。

- 表达式通常会结合级联的操作来进行属性遍历。你可以结合表达式属性AND和OR。对于属性表达式你也可以使用可支持的操作比如Between,LessThan,GreaterThan ,Like。这些支持的操作由不同的数据存储而不同，所以你需要查看你参考的文档中合适的部分。
- 方法解析支持为某些属性设置一个IgnoreCase标志(例如，findByLastnameIgnoreCase(...))或者为所有属性都支持忽略类型(通常是String实例，例如，findByLastnameAndFirstnameAllIgnoreCase(...))。是否支持ignoring cases 可能根据store不同而不同，所以相关部分在特殊库查询方法的参考文档中。
- 你可以通过增加一个OrderBy字段在按照属性来升降序的查询方法中用来静态排序。想要创建一个查询方法能够支持动态排序，请看[特殊参数处理](special_parameter_handling)