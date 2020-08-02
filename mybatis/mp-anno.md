## @MapperScan

```java
@SpringBootApplication
@MapperScan("com.zoran.mybatisplus.dao")
//@MapperScan注解可以帮助我们不用在每个dao类上添加@mapper注解
public class MybatisPlusApplication{
    ...
}
```