# 独立使用
你也可以在spring容器外使用repository组件，比如在CDI环境中，你依然需要一些spring的libraries在你的classpath中，但通常你也能以编程的方式来搭建repositories。你可以像下面示例一样使用由Spring Data模块提供各种repository持久化支持的RepositoryFactory。
```java
RepositoryFactorySupport factory = … // Instantiate factory here
UserRepository repository = factory.getRepository(UserRepository.class);
```

