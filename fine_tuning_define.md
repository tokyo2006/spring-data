# 调整repository定义

通常你的Repository interface将会继承自Repository,CrudRepository或者PagingAndSortingRepository。另外，如果你不想继承Spring Data的接口，你也能通过@RepositoryDefinition声明你的Repository interface。继承自CrudRepository会暴露一系列的方法来操作你的实体。如果你喜欢选择性的暴露某些方法，简单的从CrudRepository拷贝你想要暴露的方法到你的domain repository就可以了。

> 这允许你在Srping Data提供的功能上定义你自己的抽象。


示例7。选择性暴露CRUD方法

```java
     @NoRepositoryBean
     interface MyBaseRepository<T ID extends Serializable> extends Repository<T,ID>{
         T findOne(ID id);
         T save(T entity);
     }
     
     interface UserRepository extends MyBaseRepository<User,Long>{
         User findByEmailAddress(EmailAddress emailAddress);
     }
```

