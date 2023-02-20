# 第一部分：基础篇
## DDL语言
-   Windows链接数据库`mysql -u root -p`
-   命令的结束符用`;`或者`\\g`
```sql
1.创建数据库
create database test1;

2.选择数据库
use test1;

3.查看数据库里面的表
show tables;

4.删除数据库
drop database test1;

5.创建表
# 创建student表
use test1;
drop table if exists student; # 如果表存在，删了它
create table student(
	student_id varchar(32) not null unique comment "学生id",
	student_name varchar(32) not null comment "学生姓名",
	student_gender char(2) not null comment "学生性别",
	studnet_age int(2) not null comment "学生年龄",
	student_department char(20) not null comment "学生部门",
	primary key(student_id)  # 设置主键
);

# 创建department表
use test1;
drop table if exists department;
create table department(
	department_id varchar(32) not null unique comment "部门id",
	department_name varchar(32) not null comment "部门名字",
	department_leader varchar(10) not null comment "部门领导",
	primary key(department_id)
)engine=innodb default charset = utf8mb4;;

6.查看表的定义
describe student;

7.查看建表语句
show create table student;

8.删除表
drop table student;

9.修改表
# 修改表类型
alter table student modify student_name varchar(20);

# 增加表字段
alter table student add column student_class varchar(32) comment "学生班级";

# 删除表字段
alter table student drop column student_class;

# 字段改名
alter table student change studnet_age student_age1 int(4);

注意：change和modify都可以修改表的定义，不同的是change后面需要写两次列名，不方便。但是change的优点是可以修改列名称，modify不能。

# 修改字段排列顺序
alter table student add birth date after ename;
alter table student modify age int(3) first；
alter table student modify age1 int(4) after sal;
注意：change/first|after column这些关键字都属于MySql在标准SQL上的扩展，在其他数据库上不一定适用。

# 更改表名
alter table studnet rename studnet1;

10.建立索引
create unique index Student_Id on source(student_id);  //Student_Id是索引名字
create unique index SCno on SC(Sno ASC,Cno DESC);

11.修改索引名字
alter index Student_Id rename to StuId;               //修改索引名字

12.删除索引
drop index StuId;
```
## DML语句
```sql
1.插入记录
# 指定字段
insert into emp(ename,hiredate,sal,deptno) value("zzx1","2000-01-01","9000",1);

# 不指定字段
insert into emp value("hs","1996-11-30","2021-02-22","10000",10,2);

# 指定部分字段
insert into emp(ename,birth) value("ws","2020-01-02");

# 同时插入多个字段，用逗号隔开
insert into emp value("hh","1996-11-30","2021-02-22","10000",10,2),("yy","1996-11-30","2021-02-22","10000",10,2);

2.更新记录
update emp set sal = 100 where ename = "hh";
update emp set sal = 99, age1 = 100 where ename = "hh";
# 多表更新的字段多用在根据一个表的字段更新另一个表的字段
update dept a,emp b set a.deptname = "it",b.sal = 10 where a.deptno = b.deptno;

3.删除记录
delete from emp where ename = "zzxl";

4.查询记录
select * from emp;

# 查询不重复的记录，如果没有distinct默认all
select distinct deptno from emp;

# 条件查询
select * from emp where ename = "yy";

# 升序
select * from emp order by sal asc;

# 相同的就按照第二个排列
select * from emp where deptno = 2 order by sal,ename asc;

# 降序
select * from emp order by sal desc;

# 查看部分限制
select * from emp order by sal limit 2; //显示[0,2）
select * from emp order by sal limit 2,4; //切片，显示[2,4)

注意：limit属于MySql扩展SQL92后的语法，在其他数据库上并不能通用

# 聚合
聚合函数有：sum()、count()、max()、min()、avg()

group by 表示要进行分类聚合的字段
with rollup 表明是否对分类聚合后的结果进行再汇总
having 关键字表示对分类后的结果再进行条件的过滤

注意:having和where的区别在于，having是对聚合后的结果进行条件的过滤，而where是在聚合前就对记录进行过滤，
如果逻辑允许，我们尽可能用where先过滤记录，这样因为结果集减小，将对聚合的效率大大提高，最后再根据逻辑看是否用having进行再过滤。总之，where作用于视图，而having作用于组。

# 总数
select count(1) from emp;

# 按照deptno进行分组，计算数目
select deptno,count(1) from emp group by deptno;

# 统计部门人数，又要统计总人数  总人数是最后一行NULL的值
select deptno,count(1) from emp group by deptno with rollup;

# 选择人数大于1的部门
select deptno,count(1) from emp group by deptno having count(1)>1;

# 统计总薪水、最高和最低薪水
select sum(sal),max(sal),min(sal) from emp;

5.表链接
当需要同时显示多个表中的字段时，就可以用表连接来实现这样的功能。
内连接：仅选择出两张表中互相匹配的记录
外链接：会选出其他不匹配的记录
- -左链接：包含所有的左边表中的记录甚至是右边表中没有和它匹配的记录
- -右链接：包含所有的右边表中的记录甚至是左边表中没有和它匹配的记录

# 链接两个表查询
select ename,deptname from emp,dept where emp.deptno = dept.deptno;
select ename,sal,deptname from emp a,dept b where a.deptno = b.deptno;

# 左链接
select ename,deptname from emp left join dept on emp.deptno = dept.deptno;

# 右链接
select ename,deptname from dept right join emp on dept.deptno = emp.deptno;

6.子查询
某些情况下,当进行查询的时候,需要的条件是另外一个select语句的结果，这个时候,就要用到子查询。用于子查询的关键字主要包括in、not in、=、!=、exists、not exists 等。
嵌套查询（子查询）不能用order by， 因为order by只能作用于最终结果。

select * from emp where deptno in (select deptno from dept);

注意：(1)如果查询结果唯一，可以用"="代替"in";(2)子查询在很多情况下可以优化成表链接

7.记录联合
将两个表的数据查出来后，放在一起显示。关键字 union、union all;
union 和 union all 的主要区别是 union all 是把结果集直接合并在一起,而 union 是将 union all 后的结果进行一次 distinct,去除重复记录后的结果。
select ename from emp union select deptname from dept;
select ename from emp union all select deptname from dept;

8.范围查询
select Sage from student where Sage between 18 and 22;
select Sage from student where Sage not between 18 and 22;

9.确定集合
select Sname from studnet where Sdept in ('CS','MA','IS');
select Sname from studnet where Sdept not in ('CS','MA','IS');

10.字符匹配
# 以“刘”开头的学生姓名
select Sname from student where Sname like '刘%';

# 以“欧阳”为开头的三个字的学生
select Sname from student where Sname like '欧阳_';

# “阳”为第二个字的名字
select Sname from student where Sname like '_阳%';

11.带有exists谓词的子查询
# exists会返回逻辑值true或者fals
select Sname from student where exists (select * from sc where Sno = Student.Sno and Cno='1');
select Sname from student where not exists (select * from sc where Sno = Student.Sno and Cno='1');

12.集合查询
集合操作主要包括并操作union,交操作intersect和差操作except
```
## DCL语句
```sql
1.创建数据库用户hs
create user "hs"@"localhost" identified by "123456";

2.授权
grant select on test1.emp to "hs"@"localhost";//授予hs用户对test1数据库中emp表的查询权限
grant select on test1.emp to "hs"@"localhost";//授予hs用户对test1数据库中emp表的所有权限

3.帮助的使用
# 按照层次查看帮助
？contents

//快速查阅帮助
？ show
```
## MySql支持的数据类型
1.  关于整型：在创建表时，MySql要求指定数据宽度，如：id int(4)表示宽度为4的整形字段，如果不写，则默认宽度为int(11) 属性：auto_increment，当需要产生唯一标识符或顺序值时，用它表示自增
2.  关于定点数：dec(m,d) m称为精度，d称为标度。 表示m位数字，其中d位位于小数点后面
	### 日期时间类型
1.  如果表示"年-月-日"，通常用`date`表示
2.  如果表示"年-月-日-时-分-秒"，通常用`datetime`表示
3.  如果表示"时-分-秒"，通常用`time`表示
4.  查看当前时区 `show variables like "time_zone";`
5.  可以用`now()`函数插入当前日期
6.  修改时区为东九区 `set time_zone ="+9:00";`
### 字符串类型
1.  char和varchar的区别 都用于保存短字符串，char的长度为固定的声明的长度，varchar的长度为可变长度
2.  binary和varbinary的区别类似于char和varchar
### 枚举类型（enum）
1.  枚举类型是忽略大小写的
2.  枚举类型只允许从集合中选取单个值，而不能一次取多个值
### SET类型
1.  set和enum类型非常类似，也是一个字符串对象，里面可以包含0～64个成员
2.  set 一次可以选取多个成员
## 算数运算符
## 流程函数
## 其他常用函数
# 第二部分：开发篇
## 优化与执行
MySQL会解析查询，并创建内部数据结构（解析树），然后对其进行各种优化，包括重写查询、决定表的读取顺序，以及选择合适的索引等。用户可以通过特殊的关键字提示（`hint`）优化器，影响它的决策过程。也可以请求优化器解释（`explain`）优化过程的各个因素，使用户可以知道服务器是如何进行优化决策的，并提供一个参考基准，便于用户重构查询和schema、修改相关配置，使应用尽可能高效运行。
优化器并不关心表使用的是什么存储引擎，但存储引擎对于优化查询是有影响的。优化器会请求存储引擎提供容量或某个具体操作的开销信息，以及表数据的统计信息等。例如，某些存储引擎的某种索引，可能对一些特定的查询有优化。
对于`SELECT`语句，在解析查询之前，服务器会先检查查询缓存（`Query Cache`），如果能够在其中找到对应的查询，服务器就不必再执行查询解析、优化和执行的整个过程，而是直接返回查询缓存中的结果集。
## 并发控制
MySQL在两个层面有并发控制：服务器层与存储引擎层。
### 读写锁
解决读写经典问题的方法就是并发控制。
在处理并发读或者写时，可以通过实现一个由两种类型的锁组成的锁系统来解决问题。这两种类型的锁通常被称为共享锁（shared lock）和排他锁（exclusive lock），也叫读锁（read lock）和写锁（write lock）。
### 锁粒度
一种提高共享资源并发性的方式就是让锁定对象更有选择性。尽量只锁定需要修改的部分数据，而不是所有的资源。更理想的方式是，只对会修改的数据片进行精确的锁定。任何时候，在给定的资源上，锁定的数据量越少，则系统的并发程度越高，只要相互之间不发生冲突即可。
问题就是加锁也是需要消耗资源的。
所谓锁的策略，就是在锁的开销和数据的安全之间寻求平衡，这种平衡当然也会影响到性能。大多数商业数据库系统没有提供更多的选择，一般都是在表上施加行级锁（row-level lock），并以各种复杂的方式来实现，以便在锁比较多的情况下尽可能地提供更好的性能。
### 表锁
表锁（table lock）是MySQL中最基本的锁策略，并且是开销最小的策略。表锁会锁定整张表。一个用户在对表进行写操作（插入、删除、更新等）前，需要先获得写锁，这会阻塞其他用户对该表的所有读写操作。只有没有写锁时，其他读取的用户才能获得读锁，读锁之间是不相互阻塞的。
### 行级锁
行级锁（row lock）可以最大程度地支持并发处理（同时也带来了最大的锁开销）。
## 事物
事务就是一组原子性的SQL查询，或者说一个独立的工作单元。如果数据库引擎能够成功地对数据库应用该组查询的全部语句，那么就执行该组查询。如果其中有任何一条语句因为崩溃或其他原因无法执行，那么所有的语句都不会执行。也就是说，事务内的语句，要么全部执行成功，要么全部执行失败。
除非系统通过严格的ACID测试，否则空谈事务的概念是不够的。ACID表示原子性（atomicity）、一致性（consistency）、隔离性（isolation）和持久性（durability）。一个运行良好的事务处理系统，必须具备这些标准特征。
### 隔离级别
1. READ UNCOMMITTED（未提交读）
2. READ COMMITTED（提交读）
3. REPEATABLE READ（可重复读）
4. SERIALIZABLE（可串行化）
![[Pasted image 20230105135818.png]]
### 死锁
死锁是指两个或者多个事务在同一资源上相互占用，并请求锁定对方占用的资源，从而导致恶性循环的现象。
## 存储引擎概述
插件式存储引擎是MySOL数据库最重要的特性之一，用户可以根据应用的需要选择如何存储和索引数据、是否使用事务等。MySql默认支持多种存储引擎，以适用于不同领域的数据库应用需要，用户可以通过选择使用不同的存储引擎提高应用的效率，提供灵活的存储，用户甚至可以按照自己的需要定制和使用自己的存储引擎，以实现最大程度的可定制性。
### 常用存储引擎对比
1.  查看引擎
```sql
show engines;
show variables like "have%";
```
1.  更改引擎
```sql
# 将表ai的引擎改为innodb
alter table ai engine = innodb;
```
### MyISAM
MyISAM是MySql默认的存储引擎。MyISAM不支持事务、也不支持外键，其优势是访问的速度快，对事务完整性没有要求或者以SELECT、INSERT 为主的应用基本上都可以使用这个引擎来创建表。
### InnoDB
InnoDB存储引擎提供了具有提交、回滚和崩溃恢复能力的事务安全。但是对比 MyISAM的存储引擎，InnoDB写的处理效率差一些，并且会占用更多的磁盘空间以保留数据和索引。
1.  自动增长列 InnoDB表的自动增长列可以手工插人，但是插入的值如果是空或者0，则实际抽人的将是自动增长后的值。
2.  外键约束 MySOL支持外键的存储引擎只有InnoDB，在创建外键的时候要求父表必须有对应的索引，子表在创建外键的时候也会自动创建对应的索引。
## Schema与数据类型优化
MySQL支持的数据类型非常多，选择正确的数据类型对于获得高性能至关重要。
1. 更小的通常更好
一般情况下，应该尽量使用可以正确存储数据的最小数据类型(1)。更小的数据类型通常更快，因为它们占用更少的磁盘、内存和CPU缓存，并且处理时需要的CPU周期也更少。
2. 简单就好
简单数据类型的操作通常需要更少的CPU周期。
3. 尽量避免null
很多表都包含可为null（空值）的列，即使应用程序并不需要保存null也是如此，这是因为可为null是列的默认属性。通常情况下最好指定列为not null，除非真的需要存储null值。
如果查询中包含可为null的列，对MySQL来说更难优化，因为可为null的列使得索引、索引统计和值比较都更复杂。可为null的列会使用更多的存储空间，在MySQL里也需要特殊处理。当可为null的列被索引时，每个索引记录需要一个额外的字节，在MyISAM里甚至还可能导致固定大小的索引（例如只有一个整数列的索引）变成可变大小的索引。
通常把可为null的列改为not null带来的性能提升比较小，所以（调优时）没有必要首先在现有schema中查找并修改掉这种情况，除非确定这会导致问题。但是，如果计划在列上建索引，就应该尽量避免设计成可为null的列。
### 整数类型
有两种类型的数字：整数（whole number）和实数（real number）。
如果存储整数，可以使用这几种整数类型：tinyint，smallint，mediumint，int，bigint。分别使用8，16，24，32，64位存储空间。它们可以存储的值的范围从$-2^{n-1}$ 到$2^{n-1}-1$，其中N是存储空间的位数。
整数类型有可选的unsigned属性，表示不允许负值，这大致可以使正数的上限提高一倍。例如tinyint unsigned可以存储的范围是0～255，而tinyint的存储范围是−128～127。
有符号和无符号类型使用相同的存储空间，并具有相同的性能，因此可以根据实际情况选择合适的类型。
你的选择决定MySQL是怎么在内存和磁盘中保存数据的。然而，整数计算一般使用64位的bigint整数，即使在32位环境也是如此。
MySQL可以为整数类型指定宽度，例如int(11)，对大多数应用这是没有意义的：它不会限制值的合法范围，只是规定了MySQL的一些交互工具（例如MySQL命令行客户端）用来显示字符的个数。对于存储和计算来说，int(1)和int(20)是相同的。
### 实数类型
实数是带有小数部分的数字。然而，它们不只是为了存储小数部分；也可以使用  decimal存储比bigint还大的整数。MySQL既支持精确类型，也支持不精确类型。
float和double类型支持使用标准的浮点运算进行近似计算。如果需要知道浮点运算是怎么计算的，则需要研究所使用的平台的浮点数的具体实现。
### 字符串类型
1. varchar
   varchar类型用于存储可变长字符串，是最常见的字符串数据类型。它比定长类型更节省空间，因为它仅使用必要的空间。
   varchar需要使用1或2个额外字节记录字符串的长度：如果列的最大长度小于或等于255字节，则只使用1个字节表示，否则使用2个字节。假设采用latin1字符集，varchar(10)的列需要11个字节的存储空间。varchar(1000)的列则需要1002个字节，因为需要2个字节存储长度信息。
   varchar节省了存储空间，所以对性能也有帮助。但是，由于行是变长的，在update时可能使行变得比原来更长，这就导致需要做额外的工作。
2. char
   char类型是定长的：MySQL总是根据定义的字符串长度分配足够的空间。
   *当存储char值时，MySQL会删除所有的末尾空格*。
   char值会根据需要采用空格进行填充以方便比较。char适合存储很短的字符串，或者所有值都接近同一个长度。对于经常变更的数据，char也比varchar更好，因为定长的char类型不容易产生碎片。对于非常短的列，char比varchar在存储空间上也更有效率。
3. blob和text
   blob和text都是为存储很大的数据而设计的字符串数据类型，分别采用二进制和字符方式存储。
   实际上，它们分别属于两组不同的数据类型家族：字符类型是tinytext，smalltext，text，mediumtext，longtext；对应的二进制类型是tinyblob，smallblob，blob，mediumblob，longblob。blob是smallblob的同义词，text是smalltext的同义词。
4. enum
   有时候可以使用枚举列代替常用的字符串类型。枚举列可以把一些不重复的字符串存储成一个预定义的集合。MySQL在存储枚举时非常紧凑，会根据列表值的数量压缩到一个或者两个字节中。MySQL在内部会将每个值在列表中的位置保存为整数，并且在表的.frm文件中保存“数字-字符串”映射关系的“查找表”。
### 时间和日期类型
1. datetime：YYYYMMDDHHMMSS格式；
2. timestamp：UNIX时间戳；
3. time：HHMMSS格式；
### 位数据类型
1. bit：可以使用bit列在一列中存储一个或多个true/false值，bit列的最大长度是64个位。
2. set：如果需要保存很多true/false值，可以考虑合并这些列到一个SET数据类型，它在MySQL内部是以一系列打包的位的集合来表示的。
### 选择标识符
1. 整数
	1. auto_incerment
2. 字符串
   如果可能，应该避免使用字符串类型作为标识列，因为它们很消耗空间，并且通常比数字类型慢。
   对于完全“随机”的字符串也需要多加注意，例如MD5()、SHA1()或者UUID()产生的字符串。这些函数生成的新值会任意分布在很大的空间内，这会导致insert以及一些select语句变得很慢。
### 特殊类型数据
IP地址，它们实际上是32位无符号整数，不是字符串。用小数点将地址分成四段的表示方法只是为了让人们阅读容易。所以应该用无符号整数存储IP地址。MySQL提供INET_ATON()和INET_NTOA()函数在这两种表示方法之间转换。
## Schema设计中的陷阱
1. 太多的列
2. 太多的关联
3. 全能的枚举
   防止过度使用枚举。
## 加快alter table的速度
一般而言，大部分alter table操作将导致MySQL服务中断。我们会展示一些在DDL操作时有用的技巧，但这是针对一些特殊的场景而言的。对常见的场景，能使用的技巧只有两种：一种是先在一台不提供服务的机器上执行alter table操作，然后和提供服务的主库进行切换；另外一种技巧是“影子拷贝”。影子拷贝的技巧是用要求的表结构创建一张和源表无关的新表，然后通过重命名和删表操作交换两张表。
## 创建高性能的索引
索引（在MySQL中也叫做“键（key）”）是存储引擎用于快速找到记录的一种数据结构。这是索引的基本功能，除此之外，本章还将讨论索引其他一些方面有用的属性。
索引对于良好的性能非常关键。尤其是当表中的数据量越来越大时，索引对性能的影响愈发重要。在数据量较小且负载较低时，不恰当的索引对性能的影响可能还不明显，但当数据量逐渐增大时，性能则会急剧下降。
### 索引类型
1. B-Tree索引
B-Tree索引能够加快访问数据的速度，因为存储引擎不再需要进行全表扫描来获取需要的数据，取而代之的是从索引的根节点开始进行搜索。B-Tree索引适用于全键值、键值范围或键前缀查找。其中键前缀查找只适用于根据最左前缀的查找。
全值匹配：全值匹配指的是和索引中的所有列进行匹配。

B-Tree索引的一些限制：
- 如果不是按照索引的最左列开始查找，则无法使用索引。
- 不能跳过索引中的列；
- 如果查询中有某个列的范围查询，则其右边所有列都无法使用索引优化查找。

2. 哈希索引
哈希索引（hash index）基于哈希表实现，只有精确匹配索引所有列的查询才有效。对于每一行数据，存储引擎都会对所有的索引列计算一个哈希码（hash code），哈希码是一个较小的值，并且不同键值的行计算出来的哈希码也不一样。哈希索引将所有的哈希码存储在索引中，同时在哈希表中保存指向每个数据行的指针。

哈希索引的一些限制：
- 哈希索引只包含哈希值和行指针，而不存储字段值，所以不能使用索引中的值来避免读取行；
- 哈希索引数据并不是按照索引值顺序存储的，所以也就无法用于排序；
- 哈希索引也不支持部分索引列匹配查找，因为哈希索引始终是使用索引列的全部内容来计算哈希值的；
- 哈希索引只支持等值比较查询，包括=、IN()、<=>（注意<>和<=>是不同的操作）。也不支持任何范围查询，例如WHERE price>100；
- 访问哈希索引的数据非常快，除非有很多哈希冲突（不同的索引列值却有相同的哈希值）。当出现哈希冲突的时候，存储引擎必须遍历链表中所有的行指针，逐行进行比较，直到找到所有符合条件的行。
- 如果哈希冲突很多的话，一些索引维护操作的代价也会很高。

因为这些限制，哈希索引只适用于某些特定的场合。而一旦适合哈希索引，则它带来的性能提升将非常显著。

### 索引的优点
索引可以让服务器快速地定位到表的指定位置。
索引有如下三个优点：
1. 索引大大减少了服务器需要扫描的数据量。
2. 索引可以帮助服务器避免排序和临时表。
3. 索引可以将随机I/O变为顺序I/O。

### 高性能的索引策略
1. 独立的列
   独立的列”是指索引列不能是表达式的一部分，也不能是函数的参数。
2. 前缀索引和索引选择性
   








1.  为city表创建10个字节的前缀索引`create index cityname on city(city(10));`
2.  删除索引`drop index cityname on city;`
### 索引失效的原因
1.  不满足左前缀原则
2.  范围索引没有放在最后
3.  使用了`select *`
4.  索引列上有计算
5.  索引列上使用了函数
6.  索引类型没有加引号
7.  用`is null`和`is not null`没注意字段是否允许为空
8.  `like`查询左边有`%`
9.  使用`or`关键字时没有注意
### SQL优化小技巧
1.  避免使用`select *`
2.  用`union all`代替`union`
3.  小表驱动大表
4.  批量操作
5.  多用`limit`
6.  `in`中值太多
7.  增量查询
8.  高效的分页
9.  用链接查询代替子查询
10.  `join`的表不宜过多
11.  `join`时要注意
12.  控制索引的数量
13.  选择合理的字段类型
14.  提升`group by`的效率
15.  索引优化
## 存储过程函数
存储过程和函数是事先经过编译并存储在数据库中的一段SQL语句的集合，调用存储过程和函数可以简化应用开发人员的很多工作，减少数据在数据库和应用服务器之间的传输，对于提高数据处理的效率是有好处的。
## 条件逻辑
条件逻辑相当于在`sql`语句里写`if…else`，可以使用case表达式使用条件逻辑。
### 查找型case表达式
```sql
case
	when c1 then e1
	when c2 then e2
	when c3 then e3
	[else end]
end
```
### 简单case表达式
```sql
case v0
	when v1 then e1
	when v2 then e2
	[else ed]
end 
```
## 触发器
在改变某一个数据的同时更改另外一个数据。

# 最后
## 查看密码策略
```sql
show variables like '%validate_password_policy%';
show variables like '%validate_password_length%';
```
## 修改密码策略
```sql
set global validate_password_policy=0;set global validate_password_length=1;
```
## 更改密码
```sql
set password for 用户名@localhost = password('新密码');
```
## 外部访问
```sql
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '123456';
flush privileges;
```
## 防火墙设置
```bash
# 开启防火墙
systemctl start firewalld.service

# 关闭防火墙
systemctl stop firewalld.service

# 重启防火墙
service firewalld restart

# 指定端口范围为4400-4600通过防火墙
firewall-cmd --zone=public --add-port=4400-4600/udp --permanen

# 查看通过的端口
firewall-cmd --zone=public --list-ports

# 查看防火墙状态
firewall-cmd --state
```