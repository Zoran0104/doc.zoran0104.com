## QueryWrapper

```java
new QueryWrapper<>().eq("last_name","zoran");//1⃣️

User user = new User();
user.setLastName("zoran");
new QueryWrapper<User>(user);//2⃣️
```

上述两种方法等价，推荐后者

> **<font color=#0099ff>注意:</font>** `在MP中，条件构造器中的列名必须为数据库的列名，不能改用驼峰`



## Update

```java
// 根据 UpdateWrapper 条件，更新记录 需要设置sqlset
boolean update(Wrapper<T> updateWrapper);
// 根据 whereEntity 条件，更新记录
boolean update(T entity, Wrapper<T> updateWrapper);
// 根据 ID 选择修改，首先主键字段必须设定值，其余字段可以不用设定，为null的字段不会加到更新列表中
boolean updateById(T entity);
// 根据ID 批量更新
boolean updateBatchById(Collection<T> entityList);
// 根据ID 批量更新
boolean updateBatchById(Collection<T> entityList, int batchSize);
```

```java
		//User user = new User();
        //user.setAge(12);
        //user.setId(3);
        ////userDao.updateById(user); 1⃣️
        //userDao.update(user, new QueryWrapper<User>().eq("last_name", "guanyu"));2⃣️
        userDao.update(null, new UpdateWrapper<User>().set("age", 1111)
                .eq("last_name", "zhangwwwww"));//3⃣️
        userDao.update(null, new UpdateWrapper<>(new User()).eq("last_name", "zhangwwwww"));
		//4⃣️上述在updatewrapper传入的实体类对象里的字段构成条件，不构成更新
    }
```

## Delete

```java
// 根据 entity 条件，删除记录
int delete(@Param(Constants.WRAPPER) Wrapper<T> wrapper);
// 删除（根据ID 批量删除）
int deleteBatchIds(@Param(Constants.COLLECTION) Collection<? extends Serializable> idList);
// 根据 ID 删除
int deleteById(Serializable id);
// 根据 columnMap 条件，删除记录，多条件为and关系
int deleteByMap(@Param(Constants.COLUMN_MAP) Map<String, Object> columnMap);
```

## Select

```java
// 根据 ID 查询
T selectById(Serializable id);
// 查询（根据ID 批量查询）
List<T> selectBatchIds(@Param(Constants.COLLECTION) Collection<? extends Serializable> idList);

// 根据 entity 条件，查询一条记录,结果超出一条时抛出异常
T selectOne(@Param(Constants.WRAPPER) Wrapper<T> queryWrapper);


// 根据 entity 条件，查询全部记录
List<T> selectList(@Param(Constants.WRAPPER) Wrapper<T> queryWrapper);
// 查询（根据 columnMap 条件）
List<T> selectByMap(@Param(Constants.COLUMN_MAP) Map<String, Object> columnMap);
// 根据 Wrapper 条件，查询全部记录
List<Map<String, Object>> selectMaps(@Param(Constants.WRAPPER) Wrapper<T> queryWrapper);
// 根据 Wrapper 条件，查询全部记录。注意： 只返回第一个字段的值
List<Object> selectObjs(@Param(Constants.WRAPPER) Wrapper<T> queryWrapper);

// 根据 entity 条件，查询全部记录（并翻页）
IPage<T> selectPage(IPage<T> page, @Param(Constants.WRAPPER) Wrapper<T> queryWrapper);
// 根据 Wrapper 条件，查询全部记录（并翻页）
IPage<Map<String, Object>> selectMapsPage(IPage<T> page, @Param(Constants.WRAPPER) Wrapper<T> queryWrapper);


// 根据 Wrapper 条件，查询总记录数
Integer selectCount(@Param(Constants.WRAPPER) Wrapper<T> queryWrapper);
```

## 分页

1.配置分页插件

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

示例代码：

```java
        Page<SysMenu> sysMenuPage = sysMenuDao.selectPage(new Page<>(2, 3)
                , new QueryWrapper<SysMenu>().eq("parent_id",6));
        System.out.println(sysMenuPage.getTotal());//总条数      
				System.out.println(sysMenuPage.getPages());//总页数        
				System.out.println(sysMenuPage.getCurrent());//当前页       
				System.out.println(sysMenuPage.getTotal());//总条数
        sysMenuPage.getRecords().forEach(i-> System.out.println("i = " + i));
```

## 注入原理？

