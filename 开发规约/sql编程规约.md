# 卷首语

> 榜样很重要。  
> -- 墨菲警官《机械战警》



# SQL 风格指南

> 风格可以用来区分从好到卓越。  
> -- Bozhidar Batsov  Toptal公司副总裁，世界顶级程序员之一


# 目录

* [代码布局](#代码布局)
* [语法](#语法)
* [命名](#命名)
* [注释](#注释)
  * [注解](#注解)
* [示例模板](#示例模板)

## 代码布局

> 所有风格都又丑又难读，自己的除外。几乎人人都这样想。 把 “自己的除外”拿掉，他们或许是对的...  
> -- Jerry Coffin  GigaIO高级工程师 FORTRAN、C、C++系语言骨灰级程序员

* 使用 ***UTF-8*** 作为SQL脚本代码源文件编码。

* 所有的SQL脚本代码必须进行本地脚本文件存根 ***.sql***。命名文件方式参考[命名](#命名)！

> 忘掉你*创建/更新*到SQL中的脚本代码，这年头马航都失踪了你还能相信SQL服务器不会宕机！

* 对于开发人员，请将你的SQL脚本代码放入研发项目代码结构中，随项目代码一起保存到版本管理系统中！

* 代码一行的字符数以一屏显示全为最佳(大致为编辑器SQLServer\HANA Studio **100%** 显示时，**80-120**个字符，*刨去缩进空格等空字符后*)

> 你是在写给人看的实现逻辑，不是超市收银机在打流水单！

* 代码存在主从句或代码需要换行时，请进行代码缩进。

``` sql
-- 差
if @counter > 0 begin set @row = 1; select * from "OITM"; ... end;

-- 好
if @counter > 0
begin
    set @row = 1;
    ...
```

* 每个缩进级别使用四个空格 ***spaces*** （又名软 ***tabs***）. 不要硬 ***tabs***！这句针对的是研发，如果你用的是Windows系统恭喜你,你要小心咯！

``` sql
-- 差
if @counter > 0
begin
  set @row = 1;
  ...

-- 好
if @counter > 0
begin
    set @row = 1;
    ...
```

> 写代码如同写文章，***信达雅***那是高级别的内涵，没有排版 ～～～ “看！打印机那嫌弃的眼神！”

* 保留字(关键字) 要么全大写，要么全小写，纵观**所有的**高级语言，关键字都是**小写的**，**大写**默认都是**常量**。常量，常量，常量懂吗！

``` sql
-- 垃圾
SelEct * FroM "OITM"; 

-- 可以接受
SELECT * FROM "OITM";

-- 好
select * from "OITM";
```

> 你丫写的是代码，不是乱码！

* 一句代码请以 **;** 结尾，虽然MSSQL中无硬性要求，但是强烈推荐如此写法。

``` sql
-- MSSQL 可以接受
select * from "OITM"

-- 好
select * from "OITM";
```

> 记住MSSQL 是SQL里的一种方言，方言好吗！出了广东你再继续说粤语，试试！

* SQL 中的实体(表，列，约束，索引，视图，存储过程，函数，触发器。。。)请写在 **" "** 中。

``` sql
-- MSSQL 可以接受
select * from [OITM];

-- 可以接受
select * from OITM;

-- 好
select * from "OITM";
```

* SQL 中的实体请严格区分大小

``` sql
-- 垃圾
select * from OitM

-- 好
select * from "OITM";
```

> 不要问为什么，小名叫“狗子”的，你叫多了，他真“咬人”啊！

* 语句单词间加一个 **“ ”** 间隔开。

* 运算符与变量间加一个 **“ ”** 间隔开。

``` sql
-- 差
select * from "OITM" where "AvgPrice">100;

-- 好
select * from "OITM" where "AvgPrice" > 100;
```

> "距离产生美！" 你离那么近，“芬兰人”会弄死你的！

## 语法


## 命名

> 程式设计的真正难题是替事物命名及使缓存失效。  
> -- Phil Karlton 网景高级程序员

## 注释

> 良好的代码自身就是最佳的文档。当你要添加一个注释时，扪心自问，“如何改善代码让它不需要注释？” 改善代码，再写相应文档使之更清楚。  
> -- Steve McConnell <sup>[link](https://en.wikipedia.org/wiki/Steve_McConnell)</sup>

* 编写让人一目了然的代码然后忽略这一节的其它部分。我是认真的！

* 使用英文编写注释。

* 前导 ***--***  ***/\**** 或后导 ***\*/*** 与注释文本之间应当添加一个空格。

* 注释超过一个单词时，句首字母应当大写，并在语句停顿或结尾处使用标点符号。句号后添加一个空格。

* 避免无谓的注释。

``` sql
-- 差
set counter = 1 -- Set the value of the variable to one.
```

* 及时更新注释。过时的注释比没有注释还要糟糕。

> 好的代码就像是好的笑话 —— 它不需要解释。  
> -- Russ Olsen <sup>[link](http://russolsen.com/)</sup> 

* 避免替烂代码编写注释。重构它们使其变得一目了然。（要么做，要么不做，不要只是试试看。--Yoda）

### 注解

* 注解应该直接写在相关代码之前那行。

* 如果需要用多行来描述问题，后续行要放在 ***/\****  后面并缩排两个空格。

``` sql
/*
  Author: harold.duan
  Reseason: ***
  Date: ***
*/
...
```

## 示例模板

+ 视图(view)

  - mssql

  ``` sql
  if exists (select "name" from "sysobjects" where "name" = 'AVA_VIEW_XXX' and "xtype" = 'V')
      drop view "AVA_VIEW_XXX";
  go
  /*=======================================================================
    Create Date:2019-03-05
    Create Programmer:Harold Duan
    Create Reason:Xxx ...
  =======================================================================*/
  create view "AVA_VIEW_XXX"
  as
      select "ItemCode","ItemName" from "XXXX"
      left join
      ...;
  ```

  - hana

  ``` sql
  drop view "AVA_VIEW_XXX";
  /*=======================================================================
    Create Date:2019-03-07
    Create Programmer:Harold Duan
    Create Reason:Xxx ...
  =======================================================================*/
  create view "AVA_VIEW_XXX"
  as
      select "ItemCode","ItemName" from "XXXX"
      left join
      ...; 
  ```

+ 存储过程(procedure)

  - mssql

  ``` sql
  if exists (select "name" from "sysobjects" where "name" = 'AVA_SP_XXX' and "xtype" = 'P')
      drop procedure "AVA_SP_XXX";
  go
  /*=======================================================================
    Create Date:2019-03-07
    Create Programmer:Harold Duan
    Create Reason:Xxx ...
  =======================================================================*/
  create procedure "AVA_SP_XXX"
      @para1 nvarchar(20),
      @para2 int,
      ...
      output @error int,
      ...
  as
  begin
      ...;
      select ...;
      ...;
  end;
  ```

  - hana

  ``` sql
  /*=======================================================================
    Create Date:2019-03-07
    Create Programmer:Harold Duan
    Create Reason:Xxx ...
  =======================================================================*/
  drop procedure "AVA_SP_XXX";
  create procedure "AVA_SP_XXX" 
  ( 
    in para1 nvarchar(15),
    in para2 int,
    ...
    out error int,
    ...
  ) 
  language SQLSCRIPT 
  as
  begin
    ...;
    select ...;
    ...;
  end;
  ```

+ 函数(function)

  - mssql

    * 标量函数

    ``` sql
    if exists (select "name" from "sysobjects" where "name" = 'AVA_FN_XXX' and "xtype" = 'FN')
        drop function "AVA_FN_XXX";
    go
    /*=======================================================================
        Create Date:2019-04-25
        Create Programmer:Harold Duan
        Create Reason:Xxx ...
    =======================================================================*/
    create function "AVA_FN_XXX"
    (
        @para1 nvarchar(20),
        @para2 int,
        ...
        output @error int,
        ...
    )
    returns nvarchar(20)
    begin
        declare @ret_val as nvarchar(20);
        ...;
        select ...;
        return @ret_val;
    end;
    ```

    + 表值函数

    ``` sql
    if exists (select "name" from "sysobjects" where "name" = 'AVA_TF_XXX' and "xtype" = 'TF')
        drop function "AVA_TF_XXX";
    go
    /*=======================================================================
        Create Date:2019-04-25
        Create Programmer:Harold Duan
        Create Reason:Xxx ...
    =======================================================================*/
    create function "AVA_TF_XXX"
    (
        @para1 nvarchar(20),
        @para2 int,
        ...
        output @error int,
        ...
    )
    returns @ret_table table
    (
        "ItemCode" nvarchar(15) not null,
        "ItemName" nvarchar(100) not null,
        ...
        "Remarks" nvarchar(254),
        ...
    )
    begin
        ...;
        insert into @ret_table ("ItemCode","ItemName",...)
            select ...;
        ...;
        return;
    end;
    ```

  - hana

    + 标量函数

    ``` sql
    drop function "AVA_FN_XXX";
    /*=======================================================================
        Create Date:2019-04-25
        Create Programmer:Harold Duan
        Create Reason:Xxx ...
    =======================================================================*/
    create function "AVA_FN_XXX"
    (
        @para1 nvarchar(20),
        @para2 int,
        ...
        output @error int,
        ...
    )
    returns nvarchar(20)
    language SQLSCRIPT
    as
    ret_val nvarchar(20);
    begin
        ...;
        select ...;
        return :ret_val;
    end;
    ```

    + 表值函数

    ``` sql
    drop function "AVA_TF_XXX";
    /*=======================================================================
        Create Date:2019-04-25
        Create Programmer:Harold Duan
        Create Reason:Xxx ...
    =======================================================================*/
    create function "AVA_TF_XXX"
    (
        @para1 nvarchar(20),
        @para2 int,
        ...
        output @error int,
        ...
    )
    returns table
    (
        "ItemCode" nvarchar(15) not null,
        "ItemName" nvarchar(100) not null,
        ...
        "Remarks" nvarchar(254),
        ...
    )
    language SQLSCRIPT
    as
    begin
        ...;
        select * from ...;
    end;
    ```

## 构建者

> ”感谢我的团队，他们是最好的团队！“

<h3 align="left">
  <a href="https://github.com/EDITeam">EDITeam</a>
</h3>
<p align="left">
  <a href="https://github.com/haroldduan"><img src="https://avatars2.githubusercontent.com/u/16353458?s=400&v=4" width="70" alt="Harold.Duan" /></a>
  <a href="https://github.com/fancys"><img src="https://avatars3.githubusercontent.com/u/4202696?s=400&v=4" width="70" alt="Pancy.Fan" /></a>
  <a href="https://github.com/Aton5859"><img src="https://avatars2.githubusercontent.com/u/28555389?s=400&v=4" width="70" alt="Aaton.Kang" /></a>
  <a href="https://github.com/LsKeke"><img src="https://avatars1.githubusercontent.com/u/45222954?s=400&v=4" width="70" alt="Shuo.Liu" /></a>
</p>

## 授权

本指南基于 [MIT license](https://opensource.org/licenses/MIT) 授权许可。

## 特别鸣谢

[Ruby-China](https://ruby-china.org)