# 核心概念

在Spring Data repository 抽象的接口中心是仓库(Repository).它使得领域类的管理好比领域类的id类型就像一个类型参数，这个接口的行为主要是作为一个标记接库来捕获各种类型工作并帮助你发现接库并扩展它。CrudRepository为所管理的实体类提供复杂的CRUD功能。
事例1.CrudRepository 接口

```java
public interface CrudRepository<T, ID extends Serializable> extends Repository<T,ID>{

    <S extends T> S save(S entity); //1

    T findOne(ID primaryKey);       //2

    Iterable<T> findAll();          //3

    Long count();                   //4

    void delete(T entity);          //5

    boolean exists(ID primaryKey);  //6

    // … more functionality omitted.
}
```
1.保存所给实例

2.返回所给ID的实例

3.返回所有实例

4.返回实例数量

5.删除所给实例

6.是否存在所给的ID实例

>我们还提供了特别技术的持久性抽象,例如JpaRepository或者MongoRepository.这些接口扩展了CrudRepository和暴露了在基本持久技术中增加的潜在持久行技术接口，例如增删改查

在CrudRepository之上还有一个PagingAndSortingReporitory的抽象，它使得实体对象更容易进行分页

事例2. PagingAndSortingReposiory

```java
public interface PagingAndSortingRepository<T, ID extends Serializable>
  extends CrudRepository<T, ID> {

  Iterable<T> findAll(Sort sort);

  Page<T> findAll(Pageable pageable);
}
```

访问每页20条数据第二页的用户信息你可以简单的这样做：

```java
PagingAndSortingRepository<User, Long> repository = // … get access to a bean
Page<User> users = repository.findAll(new PageRequest(1, 20));
```

在增加的查询方法中，关键字的计数和删除查询都是有效的

事例3. 关键字计数查询

```java
public interface UserRepository extends CrudRepository<User, Long> {

  Long countByLastname(String lastname);
}
```

事例4. 关键字删除查询

```java
public interface UserRepository extends CrudRepository<User, Long> {

  Long deleteByLastname(String lastname);

  List<User> removeByLastname(String lastname);

}
```

