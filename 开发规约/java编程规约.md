# java编程规约

## 命名

【强制】代码中所有命名严禁使用拼音或英文+拼音方式，包括但不限于类名、属性名、常量名、方法名。
**说明：国际通用的拼音可视为英文，如：Beijing / alibaba / taobao 。**

【强制】包名统一使用英文小写，点分割符之间有且仅有一个自然语义单词。

【强制】类名都应遵循 UpperCamelCase 风格，但以下情形例外：DO / BO / VO / DTO / PO /  UID 。
 **类名都应为名词或动名词。**

【强制】方法名、参数名、成员变量、局部变量统一采用lowerCamelCase风格。

【强制】常量名全部大写，单词间以下划线 ‘_’ 分隔。

【强制】尽量采用单词全拼，不要嫌名字过长而使用不知所谓的简写。如：abstract : abs ; condition : cond。

【推荐】接口建议以service或able结尾

## 代码风格

【强制】严禁出现魔法值（未经预先定义的常量值）在任何地方。
[反例]
```java
    String key = "Id#EDIId_" + docEntry;
```

【强制】为方便和EDI平台对接，主键值使用Long类型，原来的Integer类型的DocEntry将被替换。

【强制】

【强制】对于类：DO / BO / VO / DTO / PO /  UID 要有注释，其他类视情况而定；方法一定要有注释。注释包括参数、返回值注释和方法作用注释。

【强制】不论语句多简单，请补全括号。

[正例]
```java
    if(...){
        return ture;
    } 
```
[反例]
```java
    if(...) return ture;
```

【强制】分支判断条件过多（三个以上），请考虑使用 switch 拆分函数。

【推荐】对应“梭鱼状”分支判断，优先过滤出不满足条件的，再执行正确的业务逻辑。

[反例]
```java
    if(...){
        if(...){
            if(...){
                if(...){
                    if(...){
                        // do something
                    }
                }
            }
        }
    }
```

[正例]
```java
    if(...){
        return ;
    }
    if(...){
        return ;
    }
    if(...){
        return ;
    }
    if(...){
        return ;
    }
    // do something
```



## 异常




## 依赖包


