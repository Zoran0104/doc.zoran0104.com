## config-location

```properties
mybatis-plus.config-location = classpath:mybatis-config.xml
```

or

```xml
<bean id="sqlSessionFactory" class="com.baomidou.mybatisplus.extension.spring.MybatisSqlSessionFactoryBean">
    <property name="configLocation" value="configuration"/> 
    ......
</bean>
```

## mapperLocations

- 类型：`String[]`
- 默认值：`[]`

MyBatis Mapper 所对应的 XML 文件位置，如果您在 Mapper 中有自定义方法(XML 中有自定义实现)，需要进行该配置，告诉 Mapper 所对应的 XML 文件位置

### typeAliasesPackage

- 类型：`String`
- 默认值：`null`

MyBaits 别名包扫描路径，通过该属性可以给包中的类注册别名，注册后在 Mapper 对应的 XML 文件中可以直接使用类名，而不用使用全限定的类名(即 XML 中调用的时候不用包含包名)

### mapUnderscoreToCamelCase

- 类型：`boolean`
- 默认值：`true`

是否开启自动驼峰命名规则（camel case）映射，即从经典数据库列名 A_COLUMN（下划线命名） 到经典 Java 属性名 aColumn（驼峰命名） 的类似映射。

注意

此属性在 MyBatis 中原默认值为 false，在 MyBatis-Plus 中，此属性也将用于生成最终的 SQL 的 select body

如果您的数据库命名符合规则无需使用 `@TableField` 注解指定数据库字段名



## global-config

### dbConfig

- 类型：`com.baomidou.mybatisplus.annotation.DbConfig`
- 默认值：`null`

MyBatis-Plus 全局策略中的 DB 策略配置，具体请查看 DbConfig

#### DbConfig

##### idType

- 类型：`com.baomidou.mybatisplus.annotation.IdType`
- 默认值：`ASSIGN_ID`

全局默认主键类型

##### tablePrefix

- 类型：`String`
- 默认值：`null`

表名前缀

##### schema

- 类型：`String`
- 默认值：`null`

schema

##### columnFormat

- 类型：`String`
- 默认值：`null`

字段 format,例: `%s`,(对主键无效)

##### tableUnderline

- 类型：`boolean`
- 默认值：`true`

表名、是否使用下划线命名，默认数据库表使用下划线命名

##### capitalMode

- 类型：`boolean`
- 默认值：`false`

是否开启大写命名，默认不开启

##### keyGenerator

- 类型：`com.baomidou.mybatisplus.core.incrementer.IKeyGenerator`
- 默认值：`null`

表主键生成器(starter 下支持`@bean`注入)

##### logicDeleteValue

- 类型：`String`
- 默认值：`1`

逻辑已删除值,([逻辑删除](https://mybatis.plus/guide/logic-delete.html)下有效)

##### logicNotDeleteValue

- 类型：`String`
- 默认值：`0`

逻辑未删除值,([逻辑删除](https://mybatis.plus/guide/logic-delete.html)下有效)

##### insertStrategy

- 类型：`com.baomidou.mybatisplus.annotation.FieldStrategy`
- 默认值：`NOT_NULL`

字段验证策略之 insert

说明:

在 insert 的时候的字段验证策略 目前没有默认值,等 {@link #fieldStrategy} 完全去除掉,会给个默认值 NOT_NULL 没配则按 {@link #fieldStrategy} 为准

##### updateStrategy

- 类型：`com.baomidou.mybatisplus.annotation.FieldStrategy`
- 默认值：`NOT_NULL`

字段验证策略之 update

说明:

在 update 的时候的字段验证策略 目前没有默认值,等 {@link #fieldStrategy} 完全去除掉,会给个默认值 NOT_NULL 没配则按 {@link #fieldStrategy} 为准

##### selectStrategy(since 3.1.2)

- 类型：`com.baomidou.mybatisplus.annotation.FieldStrategy`
- 默认值：`NOT_NULL`

字段验证策略之 select

说明:

在 select 的时候的字段验证策略: wrapper 根据内部 entity 生成的 where 条件 目前没有默认值,等 {@link #fieldStrategy} 完全去除掉,会给个默认值 NOT_NULL 没配则按 {@link #fieldStrategy} 为准



