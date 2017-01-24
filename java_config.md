# JavaConfig

你也可以在一个JavaConfig类中使用``` @Enable${store}Repositories ```声明来触发repository的构建。基于java类配置的spring容器介绍请参考此文档[JavaConfig in the Spring reference documentation](http://docs.spring.io/spring/docs/current/spring-framework-reference/html/beans.html#beans-java)
一个简单的开启Spring Data repositories的配置看上去是这样的
```java
@Configuration
@EnableJpaRepositories("com.acme.repositories")
class ApplicationConfiguration {

  @Bean
  public EntityManagerFactory entityManagerFactory() {
    // …
  }
}

```

> 示例使用了JPA声明，你也可以根据你实际使用的store模块替换掉这个声明，这同样也适用于定义的EntityManagerFactory bean.The same applies to the definition of the EntityManagerFactory bean. 你可以查阅不同的store实现配置。