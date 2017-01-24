# 为单一的repositories添加自定义行为
为了给repository添加更丰富的自定义功能，首先你需要定义一个接口和实现这个接口中的方法。使用你提供的repostiroy接口来扩展自定义接口

_Example 22. Interface for custom repository functionality_

```java
interface UserRepositoryCustom {
  public void someCustomMethod(User user);
}
```

_Example 23. Implementation of custom repository functionality_

```java
class UserRepositoryImpl implements UserRepositoryCustom {

  public void someCustomMethod(User user) {
    // Your custom implementation
  }
}
```
> 在实现的类中一定要加上**Impl**这个后缀，这点很重要

实现类本身并没有依赖任何的Spring Data，所以实现类也是一个正常的spring bean,所以你可以使用标准的依赖注入行为将它注入到其它bean中比如jdbcTemplate,诸如此类。

_Example 24. Changes to the your basic repository interface_

```java
interface UserRepository extends CrudRepository<User, Long>, UserRepositoryCustom {

  // Declare query methods here
}
```

让你的标准repository扩展为一个自定义的。组合CRUD和自定义的方法并让其在客户端可用。

## 配置

如果你使用命名空间配置，repository构件会在定义的类包中自动扫描自定义实现。这些自定义类必须按照repository-impl-postfix的命名规则命名，默认的后缀名为Impl

_Example 25. Configuration example_

```xml
<repositories base-package="com.acme.repository" />

<repositories base-package="com.acme.repository" repository-impl-postfix="FooBar" />
```

第一个配置示例会查找类com.acme.repository.UserRepositoryImpl来作为自定义repository的实现类，而第二个示例则会尝试查找com.acme.repository.UserRepositoryFooBar

## 手动连接

上面的示例展示了定义实现使用基础声明的自动连接，如何其它spring bean一样。如果自定义实现需要一些特别的连接，仅需要按照规则简单的声明和命名，构建就会参考手动定义的bean名字，而不是自动创建一个。

_Example 26. Manual wiring of custom implementations_

```xml
<repositories base-package="com.acme.repository" />

<beans:bean id="userRepositoryImpl" class="…">
  <!-- further configuration -->
</beans:bean>
```




