##	Mybatis+MP

1. dao接口继承`BaseMapper<T>`
2. `new MybatisSqlSessionFactoryBuilder().build(stream)`
   - 之前是`SqlSessionFactoryBuilder().build(stream)`

## Spring+Mybatis+MP

```xml
 	<context:property-placeholder location="jdbc.properties"/>
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource" 
          destroy-method="close">
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
        <property name="driverClassName" value="${jdbc.driver}"/>
        <property name="maxActive" value="10"/>
        <property name="minIdle" value="5"/>
    </bean>
    <bean class="com.baomidou.mybatisplus.extension.spring.MybatisSqlSessionFactoryBean" 
          id="sqlSessionFactory">
        <property name="dataSource" ref="dataSource"/>
    </bean>
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <property name="basePackage" value="com.zoran.springmp.dao"/>
    </bean>
```
## Spring Boot+MP

非特殊情况下，原先需要配置的`mybatis.mapper-locations`***以及***`mybatis.type-aliases-package`均可无需配置

```yaml
spring:
  datasource:
    type: com.alibaba.druid.pool.DruidDataSource
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/db2019?useUnicode=true
    			&characterEncoding=UTF-8&useSSL=false&serverTimezone=Asia/Shanghai
    username: root
    password: root
```

Mybatis-plus中dao类只要继承了`BaseMapper`就拥有了基本的增删改查功能

```java
public interface UserDao extends BaseMapper<User> {

}
```