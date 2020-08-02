## Spring Boot中整合配置文件

非特殊情况下，原先需要配置的***mybatis.mapper-locations***以及***mybatis.type-aliases-package***均可无需配置

```yaml
spring:
  datasource:
    type: com.alibaba.druid.pool.DruidDataSource
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/db2019
    username: root
    password: root
```

Mybatis-plus中dao类只要继承了BaseMapper就拥有了基本的增删改查功能

```java
public interface UserDao extends BaseMapper<User> {

}
```

## 在控制台显示SQL语句

```properties
logging.level.com.zoran.mybatisplus=debug
```

## 分页插件

```java
@EnableTransactionManagement
@Configuration
@MapperScan("com.zoran.mybatisplus.dao")
public class MybatisPlusConfig {
    @Bean
    public PaginationInterceptor paginationInterceptor() {
        PaginationInterceptor paginationInterceptor = new PaginationInterceptor();
        // 设置请求的页面大于最大页后操作， true调回到首页，false 继续请求  默认false
        // paginationInterceptor.setOverflow(false);
        // 设置最大单页限制数量，默认 500 条，-1 不受限制
        // paginationInterceptor.setLimit(500);
        // 开启 count 的 join 优化,只针对部分 left join
        paginationInterceptor.setCountSqlParser(new JsqlParserCountOptimize(true));
        return paginationInterceptor;
    }
}
```

```java
        Page<SysMenu> sysMenuPage = sysMenuDao.selectPage(new Page<>(2, 3)
                , new QueryWrapper<SysMenu>().eq("parent_id",6));
        System.out.println(sysMenuPage.getTotal());
        sysMenuPage.getRecords().forEach(i-> System.out.println("i = " + i));
```

> **<font color=#0099ff>注意:</font>** `在MP中，条件构造器中的列名必须为数据库的列名，不能改用驼峰`

## 多数据源配置

