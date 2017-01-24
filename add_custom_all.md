# 为所有的repositories添加自定义行为

之前的章节并没有实现当你想把一个方法添加到所有的repository接口中。要添加一个自定义行为到所有的repository中，你首先需要添加一个中介接口来声明一个共享的行为。

_Example 27. An interface declaring custom shared behavior_

```java
@NoRepositoryBean
public interface MyRepository<T, ID extends Serializable>
  extends PagingAndSortingRepository<T, ID> {

  void sharedCustomMethod(ID id);
}
```
现在你自己的repository需要扩展这个中介接口来替换之前包含方法声明的Repository接口，接着创建一个扩展持久化repository基础类的中介接口的实现类，这个类之后会作为代理自定义的repository基础类。

_Example 28. Custom repository base class_

```java
public class MyRepositoryImpl<T, ID extends Serializable>
  extends SimpleJpaRepository<T, ID> implements MyRepository<T, ID> {

  private final EntityManager entityManager;

  public MyRepositoryImpl(JpaEntityInformation entityInformation,
                          EntityManager entityManager) {
    super(entityInformation, entityManager);

    // Keep the EntityManager around to used from the newly introduced methods.
    this.entityManager = entityManager;
  }

  public void sharedCustomMethod(ID id) {
    // implementation goes here
  }
}
```

