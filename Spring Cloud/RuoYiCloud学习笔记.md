# 架构

[架构图](https://processon.com/view/link/5f4f4b2b0791296b0ef439c9)

# 部署

swagger访问地址

http://localhost:8080/swagger-ui/index.html



spring boot admin页面

http://localhost:9100/

用户名和密码的配置在nacos中

ruoyi/123456



由于是微服务项目，需要启动多个服务，占用多个端口，有可能端口被本地程序占用，导致某个微服务启动不了，可以使用

```
lsof -i:8080
# list of open files
```

命令来查看占用端口的程序，kill -9 pid杀掉

# 用户管理的实现

## 枚举值的处理方式

状态和性别这种枚举值，在数据库里，RuoYi-Cloud是用char(1)存储的

还有一个删除标记，也是char(1)，逻辑删除

返回回去，并没有做转换，直接返回数据库里的值，比如数据库存的性别是1，返回的也是1

前端如何转换显示的？

前端在请求用户列表页的同时，还请求了字典接口，system/dict/data/type/sys_normal_disable和/system/dict/data/type/sys_user_sex

前端什么时候请求了字典接口？

在dict/data.js中，定义了getDicts方法，根据字典类型，调用字典接口
![img.png](img.png)

getDicts方法在DictData组件中定义了install方法，内部调用了getDicts方法

![img_1.png](img_1.png)

DictData组件的install方法，是在main.js中调用的

```javascript
// 全局方法挂载
Vue.prototype.getDicts = getDicts
DictData.install()
```

在user/index.vue中
```vue
export default {
  name: "User",
  dicts: ['sys_normal_disable', 'sys_user_sex'],
```

默认导入了两个字典类型，然后使用了[vue-data-dict](https://github.com/moxun1639/vue-data-dict)组件进行字典的自动导入

一些列的对字典的解析转换，在这个下面

![img_2.png](img_2.png)

配置一下这个[vue-data-dict](https://github.com/moxun1639/vue-data-dict)

![img_4.png](img_4.png)

根据[vue-data-dict](https://github.com/moxun1639/vue-data-dict)的使用说明，只用定义字典类型就可以

![img_3.png](img_3.png)

具体实现在这里

![img_5.png](img_5.png)

> 学会了vue项目在浏览器里直接断点调试

小结：

总体来说，字典的转化，是在前端做的，后端接口实现比较简单，直接返回了数据库里面存储的数据。不像我们之前实现的方式，都是后端转换好后，返回给前端。

这样做的好处是什么？一般来说，前端不愿意去做数据转化，他们认为前端只要拿到数据做渲染就行了。转化属于逻辑处理，应该后端做。

> 字典转换逻辑在前端还是后端处理的问题，没有好坏之分，从clean code的角度来说，接口定义的越简单越好，后端接口返回数据库里的数据，不做任何转换，对后端来说比较清晰。

# 其他后端内容

## 导入导出的实现

高级部分：关注下默认的能力，可以做到什么程度

- 自定义导入导出标题信息
- 自定义数据处理器（对某一个字段属性处理）
- 自定义隐藏属性列
- 导出对象的子列表（可以做到自动合并单元格），比如一个人有多个角色，可以导出这个人每个角色的角色内字段
![img_6.png](img_6.png)

## 文件上传下载的实现

## 权限注解的能力

- 登录认证
- 权限认证
- 角色认证

## 事务管理

- Spring默认不会回滚检查异常，需要指定rollbackFor = Exception.class
- 在业务层捕获了异常，导致事务不生效。不应该在业务层捕获异常，应该抛出异常，在控制层统一处理

为什么需要传播行为控制？

> 事务的传播机制是指如果在开始当前事务之前，一个事务上下文已经存在，此时有若干选项可以指定一个事务性方法的执行行为。 即:在执行一个@Transactinal注解标注的方法时，开启了事务；当该方法还在执行中时，另一个人也触发了该方法；那么此时怎么算事务呢，这时就可以通过事务的传播机制来指定处理方式。


TransactionDefinition.PROPAGATION_REQUIRED	如果当前存在事务，则加入该事务；如果当前没有事务，则创建一个新的事务。这是默认值。

## 异常处理

### `@ControllerAdvice`注解或者`@RestControllerAdvice`注解

全局异常处理器就是使用`@ControllerAdvice`注解或者`@RestControllerAdvice`注解。

原理参见`RequestMappingHandlerAdapter.initControllerAdviceCache`

### `@InitBinder`注解和`@NotBlank`注解
`InitBinder`注解，用于在请求到达`Controller`前，对参数进行转化。比如对字符串参数进行去空格，对String类型的日期转换成Date类型。

> `@NotBlank`注解本身就可以对字符串参数进行去空格后验证长度是否为0，见`NotBlankValidator`类

### 无法捕获异常的几种可能

- 异常是否已被处理，即抛出异常后被catch，打印了日志或抛出了其它异常
- 异常是否非Controller抛出，即在拦截器或过滤器中出现的异常

## 参数校验

Controller方法参数前加`@Validated`注解，参数类的字段上加上各种校验的注解

### [自定义注解校验](http://doc.ruoyi.vip/ruoyi/document/htsc.html#%E8%87%AA%E5%AE%9A%E4%B9%89%E6%B3%A8%E8%A7%A3%E6%A0%A1%E9%AA%8C)

比如想做一个防止表单提交时，通过注入手段进行攻击的校验，

可以自定义一个Xss注解和校验器，可以在某个字段上加`@Xss`注解。如果要全局生效，可以在所有controller的父类controller里面使用`@InitBinder`注解来校验字符串类型

除了使用注解，也可以单独在方法里面进行验证

```java
@Autowired
protected Validator validator;

public void importUser(SysUser user)
{
    BeanValidators.validateWithException(validator, user);
}
```

### [自定义分组校验](http://doc.ruoyi.vip/ruoyi/document/htsc.html#%E8%87%AA%E5%AE%9A%E4%B9%89%E5%88%86%E7%BB%84%E6%A0%A1%E9%AA%8C)

需求来源：前面都是对一个类的属性进行校验，如果一个类的属性，在新增的时候需要校验，编辑的时候不需要校验，难道要定义另外一个相同的类？

可以使用分组校验，加上分组标记。

## 如何在SpringMVC的请求参数中使用枚举

了解了[如何在SpringMVC的请求参数中使用枚举](https://www.baeldung.com/spring-enum-request-param)。主要会用到`StringToEnumConverterFactory`这个类。

内部实现最终调用了`Enum.valueOf`

`StringToEnumConverterFactory`属于**spring-core**模块下的convert包，**spring-core**模块后续要好好学一下。

## [如何多次读取HttpServletRequest？](https://www.baeldung.com/spring-reading-httpservletrequest-multiple-times)

继承`HttpServletRequestWrapper`，将inputstream缓存起来，最后加入到`OncePerRequestFilter`的filter chain中

## [OncePerRequestFilter的作用](https://www.baeldung.com/spring-onceperrequestfilter)

## 系统日志

记录谁对什么功能，进行了什么操作

利用注解+AOP切面对方式实现

## 数据权限

### 什么是数据权限？

是指登录到系统后，可以查看哪些部门的数据

### 和菜单权限的不同

菜单权限是描述角色拥有哪些菜单，数据权限控制的更细，主要控制部门间的数据权限。

比如，销售和财务数据是不允许别的部门的人和未授权的人看到的

### 具体实现：

定义了`@DataScope`注解，及用户表和部门表的别名参数。

在Mybatis查询底部加上

```xml
${params.dataScope}
```

逻辑实现代码 `com.ruoyi.framework.aspectj.DataScopeAspect`

`DataScopeAspect`里面的代码是通过sql拼接完成的，

### 另外一种实现方式

可以是使用Mybatis的动态sql，

1、为mapper接口中参数的类型定义一个父类，父类中包含数据权限的入参字段，比如
`userAlias`，`deptAlias`，`userId`，`deptId`等，

2、新建一个数据权限的mapper接口`com.xx.xxx.DataPermissionCommonMapper`

3、为数据权限mapper接口定义一个sql statement，指定id

```xml
<mapper namespace="com.xx.xxx.DataPermissionCommonMapper">
    <sql id="data_permission">
        <if test="dataPermission.deptAlias != null">
            or #{deptAlias}.dept_id = #{deptId}
        </if>
        <if test="dataPermission.deptAlias != null and dataPermission.type == 4">
            or #{deptAlias}.dept_id in 
        </if>
    </sql>
</mapper>
```

4、在用到的数据权限的地方，通过在mapper的xml中include步骤3定义的sql，引入。

```xml
<if test="dataPermission != null">
    and (
            <include refid="com.xx.xxx.DataPermissionCommonMapper.data_permission"/>
    )
</if>
```

## 动态数据源

微服务版使用了dynamic-datasource动态多数据源组件。

- 自动切换，是通过注解
- 手动切换

```java
DynamicDataSourceContextHolder.push("slave"); // 手动切换
....业务逻辑
DynamicDataSourceContextHolder.clear();
```

具体实现可以看该组件，或者看RuoYi单机版的实现

大致思路
1. 定义数据源注解、数据源枚举
2. yml中配置多数据源
3. 在druid数据源配置中，添加另外的数据源
```java
    @Bean
    @ConfigurationProperties("spring.datasource.druid.slave")
    @ConditionalOnProperty(prefix = "spring.datasource.druid.slave", name = "enabled", havingValue = "true")
    public DataSource slaveDataSource(DruidProperties druidProperties)
    {
        DruidDataSource dataSource = DruidDataSourceBuilder.create().build();
        return druidProperties.dataSource(dataSource);
    }
```
4. 在druid数据源配置类中添加另外的数据源
```java
    @Bean(name = "dynamicDataSource")
    @Primary
    public DynamicDataSource dataSource(DataSource masterDataSource)
    {
        Map<Object, Object> targetDataSources = new HashMap<>();
        targetDataSources.put(DataSourceType.MASTER.name(), masterDataSource);
        setDataSource(targetDataSources, DataSourceType.SLAVE.name(), "slaveDataSource");
        return new DynamicDataSource(masterDataSource, targetDataSources);
    }

    /**
     * 设置数据源
     * 
     * @param targetDataSources 备选数据源集合
     * @param sourceName 数据源名称
     * @param beanName bean名称
     */
    public void setDataSource(Map<Object, Object> targetDataSources, String sourceName, String beanName)
    {
        try
        {
            DataSource dataSource = SpringUtils.getBean(beanName);
            targetDataSources.put(sourceName, dataSource);
        }
        catch (Exception e)
        {
        }
    }
```
5. 定义动态数据源切面，用于拦截方法上有数据源注解的方法，在该方法的前后进行数据源切换，设置到线程上下文中（一个ThreadLocal变量）
```java
    @Around("dsPointCut()")
    public Object around(ProceedingJoinPoint point) throws Throwable
    {
        DataSource dataSource = getDataSource(point);

        if (StringUtils.isNotNull(dataSource))
        {
            DynamicDataSourceContextHolder.setDataSourceType(dataSource.value().name());
        }

        try
        {
            return point.proceed();
        }
        finally
        {
            // 销毁数据源 在执行方法之后
            DynamicDataSourceContextHolder.clearDataSourceType();
        }
    }
```

6. 定义一个`DynamicDataSource`类，继承`AbstractRoutingDataSource`，实现`determineCurrentLookupKey`方法，并在该方法中，从线程上下文中取出数据源
```java
public class DynamicDataSource extends AbstractRoutingDataSource
{
    public DynamicDataSource(DataSource defaultTargetDataSource, Map<Object, Object> targetDataSources)
    {
        super.setDefaultTargetDataSource(defaultTargetDataSource);
        super.setTargetDataSources(targetDataSources);
        super.afterPropertiesSet();
    }

    @Override
    protected Object determineCurrentLookupKey()
    {
        return DynamicDataSourceContextHolder.getDataSourceType();
    }
}
```

## 代码生成

目的：消除重复代码，比如curd

## 定时任务

使用场景
- 数据比对
- 数据同步
- 定时生成报表
- 定时清理数据

数据表里保存了定时任务的元数据信息，
定时任务会在系统启动或者新增定时任务时，加入到内存中，

启用时，会去调用具体的任务类的方法

官方文档给出了一些cron表达式的例子，可以在以后写cron表达式时，根据需求[参考](http://doc.ruoyi.vip/ruoyi/document/htsc.html#%E5%AE%9A%E6%97%B6%E4%BB%BB%E5%8A%A1)下

## 接口文档

Swagger接口文档RuoYi Cloud提供的使用方式很具体，可以在需要查阅的时候[参考](http://doc.ruoyi.vip/ruoyi/document/htsc.html#%E7%B3%BB%E7%BB%9F%E6%8E%A5%E5%8F%A3)。

## 防重复提交

目的：防止会话重放攻击

使用：方法上加`@RepeatSubmit`注解

## 国际化

了解即可

配置不同的国际化资源，在切换时会用到

## 新建子模块

需要新建时，照着文档操作即可

