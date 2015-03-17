# 查询方法

标准的CRUD功能的repositories通常在数据存储底层都有各种查询。使用Spring Data，声明这些查询有以下四步流程。

1. 声明一个继承于Repository的接口或者一个子接口并注入实体类和它的ID类型
   ```java
   interface PersonRepository extends Repository<User, Long> { … }
   ```
1. 
在接口中声明查询方法
```java
interface PersonRepository extends Repository<User, Long> {
  List<Person> findByLastname(String lastname);
}
```
1. 
使用Spring来为这些接口创建代理实例。也可以通过[JavaConfig](java_config.md): 

```java
import org.springframework.data.jpa.repository.config.EnableJpaRepositories;

@EnableJpaRepositories
class Config {}
```

或者通过[XML配置](xml_configuration.md):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xmlns:jpa="http://www.springframework.org/schema/data/jpa"
   xsi:schemaLocation="http://www.springframework.org/schema/beans
     http://www.springframework.org/schema/beans/spring-beans.xsd
     http://www.springframework.org/schema/data/jpa
     http://www.springframework.org/schema/data/jpa/spring-jpa.xsd">

   <jpa:repositories base-package="com.acme.repositories"/>

</beans>
```

JPA的命名空间也在这个例子中。如果你正在使用其他抽象repository，你需要改变相应的命名空间来替换jpa的声明支持你得存储模块，例如mongodb.并且注意JavaConfig的变量并不需要配置一个明确的包如同默认使用的声明类。定制包扫描。

4.
获取repository实例注入并使用它。
```java
public class SomeClient {

  @Autowired
  private PersonRepository repository;

  public void doSomething() {
    List<Person> persons = repository.findByLastname("Matthews");
  }
}
```

以下的章节将会详细解释这些步骤

