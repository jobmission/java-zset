# java-zset
redis的zset的java实现，包含3个版本，Long2ObjectZset, Object2LongZset, GenericZSet。  
GenericZSet是基准实现，Long2ObjectZset, Object2LongZset是GenericZSet特化实现，以减少大量的拆装箱。  

java-zset实现了redis zset中的常用命令，且结合java语言自身的特性，进行了大量优化，包括：   
1. score不再限定为double类型，支持泛型score。
2. 可自定义ScoreComparator, KeyComparator，使得实现逆序排行榜更加容易，而不是让你总是使用reverse系列接口。
此外，扩展zset较为容易，你可以在理解后自行添加需要的特性。

### 引入项目
```
    <dependency>
        <groupId>io.github.hl845740757</groupId>
        <artifactId>java-zset</artifactId>
        <version>1.6</version>
    </dependency>
```
### 1.6
[#3](https://github.com/hl845740757/java-zset/issues/3) 小分数区间段时zadd通过比较score是否相等，以减少增删操作。


### 1.4~1.5
修改包名为个人域名(wjybxx.cn)，发布到maven中央仓库。  
PS: 注册了1个10年的域名，不过暂时未备案，也未搭建网站。

#### 1.3 fastItr
使用普通迭代器和普通zscan时，你可以保留返回的Entry对象，这些对象是新的不会被复用的；但使用快速迭代器时，你不可以保留返回的Entry对象的引用。

#### 主要参考
 * [redis 源码](https://github.com/antirez/redis)
 * [lua 版zset实现](https://github.com/XanthusL/zset)
 * [go 版zset实现](https://github.com/liyiheng/zset)
 * [java版zset实现](https://github.com/gaopan461/java-zset)
 * [Redis 为什么用跳表而不用平衡树](https://juejin.im/post/57fa935b0e3dd90057c50fbc)
 
#### 为什么还要自己实现一遍呢？
上面提到的源码，主要问题：代码可读性极差，又缺乏注释，导致理解起来十分困难（看得我头疼）。因此在我的实现中，除了添加丰富的注释外，还进行了适当的重构，代码的可读性有着极大的提升，方便小伙伴们学习。