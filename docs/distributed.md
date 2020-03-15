# 分布式问题

Topics About Distributed System

## 理论

**分布式系统**的理论更准确地说，是分布式数据存储系统(Distrituted Data Store)理论，因为主要是围绕数据冲突问题的。一般系统的核心都是数据，所以一般分布式系统都是分布式数据存储系统

### CAP 理论
对于分布式数据存储系统，有三个性质无法同时完美满足：

- Consistency 一致性：所有读都读到最新的写 或者 error
- Availability 可用性：所有请求读到非error的结果，但不一定是最新的写入
- Partial tolerence 分区容忍性：当系统的节点间的网络有任意丢包或延迟时，系统仍能正确工作。

**三者只能取其二**。

在应用中，因为需要扩展，网络时不可避免的，通常是考虑当网络问题出现时，对可用性（A）和一致性（C）的取舍。

而即使网络正常，因为有延迟，又有了对于延迟 (L)antency 和 一致性(C)的取舍。发展成了PACELC

### PACELC 理论 
当存在分区(P)时：

- 出现网络异常时，要在 可用性(A)和一致性(C)中取舍，或者(Else) 
- 在网络正常时，要在 延迟（L）和一致性(C)中取舍。

RDBMS通常是一致性优先，而NoSQL则演化出了方案：「BASE」

### BASE
Basically Available, Soft state, Eventually consistent
基本可用，软状态，最终一致性。

**BA** 读和写操作都尽可能可用，但是不保证任何一致性，写了可能冲突而无效，读得未必是最新的。

**S** 没有了一致性保证，一段时间后，我们有一定可能性知道数据当前的状态，因为状态可能还未收敛。

**E** 我们在输入之后如果等待足够久，那么最终我们可以知道数据是什么状态，并且未来的读到的结果会和我们期望的结果一致。


最终一致性(EC) 经常被批评增加了分布式的复杂度。一个原因是EC的保证不够精确（不知道什么时候收敛） 并不是一个安全的保证：收敛前，可能读到任何值。 于是有了**SEC**


### SEC 强最终一致性
strong eventual consistency (SEC) 
增加了一条保证：2个收到过相同的更新操作组集合（不论集合的顺序）的节点的状态是一样的。 而且，系统是单调变化的（monotonic），应用永远不会收到回滚。
SEC常见的实现方法叫做：「CRDT」。

### CRDT
Conflict-free replicated data types，我自己翻译成： 备份无冲突数据类型。

阿里云的实现：https://yq.aliyun.com/articles/635632?utm_content=m_1000015503

## 概念

### 事务
[数据库](#db)事务简称事务(transaction)。

定义：是指关系型数据库管理系统(DBMS)中的事务，是一种特殊操作。数据库能让一个事务在执行时，能满足[ACID](#acid)4个性质。

目的：事务可以让数据库的一组操作变得「可靠」。具体来说是「隔离」并发访问数据库的不同请求，如果隔离失败，那么这次请求应该返回错误。

举例：转账事务：从一个人的账户数据里扣钱，并往另一个人账户里加钱。


- **可靠** 指当发生了系统错误或者操作执行一半被停止了，能在恢复时并保持数据库的「一致性」。
- **隔离** 见ACID中的隔离性。
- **一致性** 见ACID中的一致性。

### ACID：
**原子性（atomicity）** 一个事务是一个不可分割的工作单位，事务中执行的操作要么都成功，要么都失败。

**一致性（consistency）** 有三种解释，通常指第二条，不过一般数据库是三点全部能满足：

- 以后事务提交成功后，新的事务可以看到它产生的效果。
- 事务执行完数据应该仍满足数据库中定义的规则限制。
- 保证事务中的每一项操作的正确、合法、有效。

**隔离性（isolation）** 数据库一般会提供不同「隔离级别」。最严格的隔离是指：并发执行的事务结果跟他们按提交顺序逐个执行的结果一样。隔离性是「并发控制」的主要问题。

**持久性（durability）** 也称永久性（permanence），指一个事务一旦提交，它对数据库中数据的改变就应该是永久性的。接下来的其他操作或故障不应该对其有任何影响。


### 隔离级别 (isolation levels)：

越高的隔离性意味着越低的并发，有4个级别:

**Read Uncommitted（读取未提交内容）** 所有事务都可以看到其他未提交事务的执行结果。本隔离级别很少用于实际应用，因为它的性能也不比其他级别好多少。读取未提交的数据，也被称之为脏读（Dirty Read）。

**Read Committed（读取提交内容）** 这是大多数数据库系统的默认隔离级别（但不是MySQL默认的）。它满足了隔离的简单定义：一个事务只能看见已经提交事务所做的改变。这种隔离级别 也支持所谓的不可重复读（Nonrepeatable Read），因为同一事务的其他实例在该实例处理其间可能会有新的commit，所以同一select可能返回不同结果。

**Repeatable Read（可重读）** 这是MySQL的默认事务隔离级别，它确保同一事务的多个实例在并发读取数据时，会看到同样的数据行。不过理论上，这会导致另一个棘手的问题：「幻读」 （Phantom Read）。

**Serializable （串行化）** 最高级别，不会有幻读。等价于按序逐个执行。

- **幻读** 简单的说，指当用户读取某一范围的数据行时，另一个事务又在该范围内插入了新行，当用户再读取该范围的数据行时，会发现有新的“幻影” 行。InnoDB和Falcon存储引擎通过多版本并发控制（MVCC，Multiversion Concurrency Control）机制解决了该问题。

|Isolation level \\ Read phenomena | Lost updates | Dirty reads | Non-repeatable reads | Phantoms|
|---|---|---|---|---|
|Read Uncommitted | don't occur | may occur | may occur | may occur|
|Read Committed | don't occur | don't occur | may occur | may occur|
|Repeatable Read | don't occur | don't occur | don't occur | may occur|
|Serializable | don't occur | don't occur | don't occur | don't occur|

### db数据库：
database，一般特指关系型数据库比如Oracle、MySQL、SQLserver，区别于[非关系型数据库](#nosql)，也可以泛指所有类型数据库。因为数据库不只是一个库，还包含了一套管理系统，所以完整叫做：数据库管理系统：英文缩写DBMS。

### NoSQL非关系型数据库: 
非关系型数据库如redis, memcache, mongoDB，区别于关系型，可以理解为不用SQL语句，所以NoSQL。


## 分布式锁
分布式系统使用同一个资源时：分布式锁：可用性程度，可重入问题，性能问题，是否阻塞，有实效时间

### 实现方案
1. 用数据库唯一键索引，或者行锁；
2. 用缓存 如redis
3. 用强一致的系统：ZK

### 乐观锁和悲观锁
按场景优化：对冲突概率的判断

因为网络的不稳定性，服务会尽量设计得无状态，有幂等性，对使用方更友好