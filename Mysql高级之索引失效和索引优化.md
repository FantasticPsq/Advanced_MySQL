## `Mysql`高级之索引失效和索引优化 ##

如何避免索引失效和索引优化：

1. 全值匹配我最爱：尽可能进行全值匹配，即查询个数与顺序和所建索引一致。
2. 最佳左前缀法则：复合索引的第一个不能少，否则索引失效。即查询从索引的最左前列开始并且**不跳过中间的列**
3. 不在索引列上做任何操作（计算，函数，（自动或者手动）类型转换），否则会导致索引失效而转向全表扫描。
4. 存储引擎不能使用索引中范围条件右边的列
5. 尽量使用覆盖索引（只访问索引的查询（索引列和查询列一致）），减少`select *`。
6. `Mysql`在使用不等于（1=或者<>)的时候无法使用索引，会导致全表扫描。
7. `is null`和`is not null`也无法使用索引
8. `like`以通配符开头('`%abc...`')时，`mysql`索引会失效而变全表扫描。用覆盖索引可以稍微缓解此问题。
9. 字符串不加单引号索引会失效
10. 少用`or`，用它来连接时索引会失效。

所以尽量遵循以上优化原则。



