# 流查询结果

查询方法能对以JAVA 8的Stream<T>为返回的结果进行逐步处理。而不是简单地包装查询结果在被用来执行流的流数据存储特定的方法。

示例11。以JAVA 8的Stream<T>来进行查询的流处理结果

```java


     @Query("select u from User u")
     Stream<User> findAllByCustomQueryAndStream();

     Stream<User> readAllByFirstnameNotNull();

     @Query("select u from User u")
     Stream<User> streamAllPaged(Pageable pageable);
```

> 一个数据流可能包裹底层数据存储特定资源，因此在使用后必须关闭。 你也可以使用close()方法或者JAVA 7 try-with-resources区块手动关闭数据流。


示例12.在try-with-resources块中操作一个Stream<T>

```java
     try(Stream<User stream = repository.findAllByCustomQueryAndStream()){
         stream.forEach(...);
     }
```

> 当前不是所有的Spring Data模块都支持Stream<T>作为返回类型
