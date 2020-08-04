> **<font color=#0099ff>注意:</font>** `在MP中，条件构造器中的列名必须为数据库的列名，不能改用驼峰`

### Update

```java
// 根据 UpdateWrapper 条件，更新记录 需要设置sqlset
boolean update(Wrapper<T> updateWrapper);
// 根据 whereEntity 条件，更新记录
boolean update(T entity, Wrapper<T> updateWrapper);
// 根据 ID 选择修改，首先主键字段必须设定值，其余字段可以不用设定，为null的字段不会加到更新列表的字段中
boolean updateById(T entity);
// 根据ID 批量更新
boolean updateBatchById(Collection<T> entityList);
// 根据ID 批量更新
boolean updateBatchById(Collection<T> entityList, int batchSize);
```

##### 参数说明

|     类型      |    参数名     |               描述               |
| :-----------: | :-----------: | :------------------------------: |
|  Wrapper<T>   | updateWrapper | 实体对象封装操作类 UpdateWrapper |
|       T       |    entity     |             实体对象             |
| Collection<T> |  entityList   |           实体对象集合           |
|      int      |   batchSize   |           更新批次数量           |

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