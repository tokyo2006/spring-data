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