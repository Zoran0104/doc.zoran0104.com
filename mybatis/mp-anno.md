## @MapperScan

```java
@SpringBootApplication
@MapperScan("com.zoran.mybatisplus.dao")
//@MapperScan注解可以帮助我们不用在每个dao类上添加@mapper注解
public class MybatisPlusApplication{
    ...
}
```

## @TableId

```java
@TableId(type = IdType.AUTO)
```

>  使用该注解可以设置主键增长类型，并且***<font color=#0099ff>在insert后也会自动回传将主键值注入对象的该属性，在insert中当字段为null时，默认是不添加到insert后的列表，主键字段除外</font>***

|   type值    |                             描述                             |
| :---------: | :----------------------------------------------------------: |
|    AUTO     |                         数据库ID自增                         |
|    NONE     | 无状态,该类型为未设置主键类型(**<u>注解里等于跟随全局,全局里约等于 INPUT</u>**) |
|    INPUT    |                    insert前自行set主键值                     |
|  ASSIGN_ID  | 分配ID(主键类型为Number(Long和Integer)或String)(since 3.3.0),使用接口`IdentifierGenerator`的方法`nextId`(默认实现类为`DefaultIdentifierGenerator`雪花算法) |
| ASSIGN_UUID | 分配UUID,主键类型为String(since 3.3.0),使用接口`IdentifierGenerator`的方法`nextUUID`(默认default方法) |

## @TableField

|   属性   |  类型   | 必须指定 | 默认值 |         描述         |
| :------: | :-----: | :------: | :----: | :------------------: |
| `value`  | String  |    否    |   ""   |     数据库字段名     |
| `exist`  | boolean |    否    |  true  |  是否为数据库表字段  |
| `select` | boolean |    否    |  true  | 是否进行 select 查询 |
|  其余见官网         |

> 当数据库表的字段名为数据库保留关键字时，例如`desc`等，使用`TableField`注解时需加上\`  \` 
>
> Ex:
>
> xml配置中：正确：\`desc\` = #{desc}			错误：desc#{desc}
>
> ```java
> @TableField("`desc`")
> private String desc;
> ```