

[toc]

> 编码规范的意义：代码美观，易于阅读理解/降低维护成本/降低出错概率/提升代码执行效率 感触：简单才是美

### :one:命名

**对象命名**= `对象前缀+模块名+对象标识` v_act_custinfo

| 对象类型               | 对象前缀 | 格式                |
| ---------------------- | -------- | ------------------- |
| 临时表 temporary table | t        |                     |
| 视图 view              | v        | v_表名              |
| 序列 sequence          | s        | s_表名              |
| 索引 index             | idx      | idx_表名_每列首字母 |
| 主键 primary key       | pk       | pk_表名             |
| 过程 procedure         | p        |                     |
| 函数function           | f        |                     |

**变量命名** = `变量前缀+变量标识`

| 变量类型     | 前缀 | 示例         |
| ------------ | ---- | ------------ |
| 局部变量     | v    | v_begin_date |
| 输入输出参数 | p    | p_oc_date    |

**常用英文简写**(原则上简写应不产生歧义)
| 全写         | 简写 |
| ------------ | ---- |
| information  | info |
| customer     | cust |
| description  | desc |
| destination  | dest |
| source       | src  |
| config       | cfg  |
| organization | org  |
| control      | ctrl |
| department   | dept |
| employee     | emp  |
| business     | biz  |

>通常不应使用**数字**/**特殊字符**来定义标识符
>
>避免使用数据库**关键字**&**保留字** 如: count
>
>长度<=**30**个字符
### :two:书写
**缩进**

- 缩进2空格，同一条语句中每个关键字单独成行，右对齐

   <img src="https://img-blog.csdnimg.cn/5f037d412b33459b97ae8e0095a1d16d.png" width=33%/>

**换行**

1. 段语句单独成行
2. 程序块之间用一个空行隔开
3. 较长语句适当换行
4. 在低优先级操作符处，操作符放在行首，并适当缩进
5. 关键字独立成行：`DECLARE` `AS` `RETURN` `BEGIN` `END` `EXCEPTION`
   <img src="https://img-blog.csdnimg.cn/ae1a61a11392409d87bd7a873a91868d.png"  width=30%/>

**格式**

1. 除字符串外，统一使用小写字符书写

2. 操作符前后应以空格分隔，间隔符之后应以空格分隔

    <img src="https://img-blog.csdnimg.cn/c83aee43c0f54177826a6f01b130aa70.png"   width=36%/>

3. insert语句中，select中的字段应与insert中的字段在位置上——对应

    <img src="https://img-blog.csdnimg.cn/fc2b6c2d56ff46659222e9064dbee886.png"   width=50%/>



### :three:注释

1. 脚本文件、函数、过程头部应加注释

2. 注释内容包括:创建者、创建日期、功能描述、修改记录等

    <img src="https://img-blog.csdnimg.cn/e193895219c14b91a7c388b6d7663c1d.png"  width=40% />

3. 注释应紧靠其描述的代码，在代码的上方或者右方

    <img src="https://img-blog.csdnimg.cn/0b6826ff3e994292b2f06f0b53826d81.png"  width=40% />

4. 注释与所描述的代码进行同样的缩进

5. 通过对函数、过程、变量等进行合理命名，使其成为自注释的



### :four:语法
1. 使用SQL99语法标准，连接条件写在 `on` 里，过滤条件写在 `where` 里

    <img src="https://img-blog.csdnimg.cn/bf27eac21eae471e801a86155aafb215.png"  width=30%/>

2. 不允许使用 `select *`，将需要的字段一一列出

    <img src="https://img-blog.csdnimg.cn/32fc9b1dc61e4d3bb199903d40136ebd.png"  width=25%/>

3. insert语句中必须列出要插入的字段名

    <img src="https://img-blog.csdnimg.cn/a4d0ecef8cac4447baf05c8dbd140fca.png"  width=20%/>

4. 当sql中涉及多个表时，字段名应+前缀表名/表别名，别名不要重复

    <img src="https://img-blog.csdnimg.cn/e5da460ca8ca49b3b2f75a87a5a5ab6f.png"  width=40%/>

5. 尽量使用静态sql，少用动态sql

    <img src="https://img-blog.csdnimg.cn/1041bc10429641c1b65e09c97f6a2e2d.png"  width=50%/>

6. 使用通用语法和函数. 如用 `case` 代替 `decode` (Oracle特有函数，放到MySQL里就不会识别)

7. 不使用 `goto` (跳跃性)语句来控制流程

8. 少用游标(代码效率差)



### :five:优化

1. where中应避免隐式转换，避免对索引列使用丞数

    <img src="https://img-blog.csdnimg.cn/356680a667a84cf297bb39c266ac33d7.png"   width=60%/>

2. 表的更新操作用 `merge` 代替 `update`

    <img src="https://img-blog.csdnimg.cn/b3ea5f38b7b7433fb0456e6fb27df78f.png"   width=60%/>

3. 避免函数频繁执行

    <img src="https://img-blog.csdnimg.cn/b3f36e0e4daa44f0b031d80cc38e3c79.png"   width=60%/>

4. 尽量避免使用 `or` 操作符

    <img src="https://img-blog.csdnimg.cn/b18c1c485ef448f58d581b7fe0336c70.png"   width=40%/>

5. 动态sql应使用绑定变量

    <img src="https://img-blog.csdnimg.cn/cf5c316de7ae458d8e32135257968d09.png"   width=30%/>

6. 判断存在性时，要加上 `rownum=1`

    <img src="https://img-blog.csdnimg.cn/ee4d80e52bf64560843bef76360b5cd9.png"   width=30%/>

7. 变量赋值尽量用 `:=`，比 `select into` 快

    <img src="https://img-blog.csdnimg.cn/e45ad1d772d740e997557c6432eed602.png"   width=50%/>

8. 避免不必要的排序，如可以用 `union all` 时就不要用 `union`

9. 不要随意 `commit`，应保证事务完整性