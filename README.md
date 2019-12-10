# Database-Summary

## 数据库引擎：
### MyISAM：
 
    1)基于ISAM存储引擎，并在其基础上进行扩展，不支持事务<br/>
    2)不支持外键（<kdb>Foreign_Key</kdb>），
    3)读写操作属于串行模式，如果对同一张表进行读写操作时，写操作的进程会优先获取锁，因此不适合执行有大量读取和更新操作的数据，适合读操作多的少量数据。<br/>
    4)采用表级锁（共享锁和排它锁），这类锁的特点是：资源开销少，加锁的速度快，不会出现死锁，并发的程度低，加锁的粒度大，冲突概率比较高。<br/>
    5)不保存表记录数，执行select count(1) from xxx时会进行全表扫描。<br/>
    6)创建数据库将会产生3个文件，.frm存储表结构，.MYD存储表数据，.MYI存储表索引，索引被压缩过。<br/>
### InnoDB:
  
    1)为Mysql在事务提交，回滚，灾难恢复等安全方面提供了支持。<br/>
    2)支持外键(<kdb>Foreign_Key</kdb>)<br/>
    3)与Mysql完全整合，是为了处理巨大量数据而设计。<br/>
    4)支持表级锁与行级锁，默认为行级锁。行级锁开销大，加锁慢，锁粒度小，冲突概率低，并发度高，会出现死锁。表级锁一般由数据库内部进行，因此不需要特别的关注。<br/>
    5)保留表记录数，当执行select count(1) from xxx时不会进行全表扫描。<br/>
    6)索引与数据紧密捆绑，索引没有压缩。在索引方面的内存使用率，不如MyISAM。<br/>

### 比较：

  |          |     MyISAM     |     InnoDB     |
  | :----: | :----: | :----: |
  | 存储限制 | 无限制 | 64TB |
  | 锁机制 | 表锁 | 表锁·行锁 |
  | 死锁 | 不会 | 会 |
  | B树索引 | 是 | 是 |
  | 全文索引 | 支持 |  |
  | 集群索引 | 不支持 | 支持 |
  | 数据可压缩 | 支持 | 不支持 |
  | 空间使用率 | 低 | 高 |
  | 内存使用率 | 低 | 高 |
  | 批量插入速度 | 高 | 低 |
  | 外键 | 不支持 | 支持 |
  | 事务 | 不支持 | 支持 |
