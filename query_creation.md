# 创建查询

基础Spring Data repository内置的查询生成器机制对于创建实体仓库的约束查询是有用的，它会从方法名中去掉find...By,read...By,query...By,count...By和get...By这些前缀并解析剩下的内容.