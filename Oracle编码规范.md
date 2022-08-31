#  Oracle编码规范

编码规范的意义：代码美观，易于阅读理解/降低维护成本/降低出错概率/提升代码执行效率

### 命名

**对象命名**=对象前缀+模块名+对象标识 v_act_custinfo

对象类型								对象前缀		格式
临时表(temporary table)      t
视图(view )							 v					`v_表名`
序列(sequence)					 s				   `s_表名`
索引( index)							idx			   `idx_表名_每列首字母`
主键(primary key )				pk				`pk_表名`
过程(procedure)					p
函数(function)						f 

**变量命名**
通常由变量前缀+变量标识组成

变量类型			前缀		示例
局部变量			v			v_begin_date
输入输出参数	p			p_oc_date

**常用英文简写**(原则上简写应不产生歧义)

全写				简写
information	 info
customer		 cust
description	  desc
destination	  dest
source			  src
config			   cfg
organization   org
control			 ctrl
department	dept
employee		emp
business		  biz

**注**：

通常不应使用数字或特殊字符来定义标识符
避免使用数据库关键字和保留字 如: count
长度不超过30个字符

### 书写

**缩进**

缩进2空格，同一条语句中每个关键字单独成行，右对齐

 <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220824210748569.png" alt="image-20220824210748569" style="zoom: 33%;" /><img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826054734009.png" alt="image-20220826054734009" style="zoom:25%;" />

**换行**

1. 段语句单独成行
2. 程序块之间用一个空行隔开
3. 较长语句适当换行
4. 在低优先级操作符处，操作符放在行首，并适当缩进
5. 关键字独立成行：DECLARE、AS、RETURN、BEGIN、END、EXCEPTION

 <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826054734009.png" alt="image-20220826054734009" style="zoom:33%;" />

 <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826055437188.png" alt="image-20220826055437188" style="zoom:33%;" />

**书写**

1. 除字符串外，统一使用小写字符书写
2. 操作符前后应以空格分隔，间隔符之后应以空格分隔

 <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826055636037.png" alt="image-20220826055636037" style="zoom:33%;" />

3. insert语句中，select中的字段应与insert中的字段在位置上——对应

 <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826055725497.png" alt="image-20220826055725497" style="zoom:33%;" />

 <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826055756719.png" alt="image-20220826055756719" style="zoom:33%;" />查询较多时把字段分行

### 注释

1. 脚本文件、函数、过程头部应加注释
2. 注释内容包括:创建者、创建日期、功能描述、修改记录等

 <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826060022206.png" alt="image-20220826060022206" style="zoom:33%;" />

3. 注释应紧靠其描述的代码，在代码的上方或者右方

 <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826060203602.png" alt="image-20220826060203602" style="zoom:33%;" />

4. 注释与所描述的代码进行同样的缩进
5. 通过对函数、过程、变量等进行合理命名，使其成为自注释的

### 语法

1. 使用SQL99语法标准，连接条件写在on里，过滤条件写在where里

     <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826060951953.png" alt="image-20220826060951953" style="zoom:33%;" />

2. 不允许使用select *，将需要的字段一一列出

     <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826061010299.png" alt="image-20220826061010299" style="zoom:33%;" />

3. insert语句中必须列出要插入的字段名
    <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826060748750.png" alt="image-20220826060748750" style="zoom:33%;" />

4. 当sql中涉及多个表时，字段名应+前缀表名/表别名，别名不要重复

     <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826061046575.png" alt="image-20220826061046575" style="zoom:33%;" />

5. 尽量使用静态sql，少用动态sql

     <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826061549188.png" alt="image-20220826061549188" style="zoom:33%;" />

6. 使用通用语法和函数. 如用case代替decode(Oracle特有函数，放到MySQL里就不会识别)

7. 不使用goto(跳跃性)语句来控制流程

8. 少用游标(代码效率差)

### 优化

1. where中应避免隐式转换，避免对索引列使用丞数 <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826062024633.png" alt="image-20220826062024633" style="zoom:33%;" />走全表扫描

2. 表的更新操作用merge代替update

     <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826062301709.png" alt="image-20220826062301709" style="zoom:33%;" />

3. 避免函数频繁执行

    <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826062422977.png" alt="image-20220826062422977" style="zoom:33%;" />1亿次要执行1天多

4. 尽量避免使用or操作符

     <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826062635030.png" alt="image-20220826062635030" style="zoom:33%;" />

5. 动态sql应使用绑定变量

     <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826062807249.png" alt="image-20220826062807249" style="zoom:33%;" />

6. 判断存在性时，要加上rownum=1

     <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826062858030.png" alt="image-20220826062858030" style="zoom:33%;" />

7. 变量赋值尽量用:=，比select into快

     <img src="C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20220826062957866.png" alt="image-20220826062957866" style="zoom:33%;" />

8. 避免不必要的排序，如可以用union all时就不要用union
9. 不要随意commit，应保证事务完整性

感触：简单才是美