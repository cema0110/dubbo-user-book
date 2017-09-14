# 注解配置

需要 `2.2.1` 以上版本支持  

## 服务提供方

### 注解

```java
import com.alibaba.dubbo.config.annotation.Service;
 
@Service(version="1.0.0")
public class FooServiceImpl implements FooService { 
    // ...
}
```
    
### XML 配置

``` xml
<!-- 公共信息，也可以用dubbo.properties配置 -->
<dubbo:application name="annotation-provider" />
<dubbo:registry address="127.0.0.1:4548" />
 
<!-- 扫描注解包路径，多个包用逗号分隔，不填pacakge表示扫描当前ApplicationContext中所有的类 -->
<dubbo:annotation package="com.foo.bar.service" />
```

## 服务消费方

### 注解

``` java
import com.alibaba.dubbo.config.annotation.Reference;
import org.springframework.stereotype.Component;
 
@Component
public class BarAction { 
    @Reference(version="1.0.0")
    private FooService fooService;
}
```

### XML 配置

``` xml
<!-- 公共信息，也可以用dubbo.properties配置 -->
<dubbo:application name="annotation-consumer" />
<dubbo:registry address="127.0.0.1:4548" />
 
<!-- 扫描注解包路径，多个包用逗号分隔，不填pacakge表示扫描当前ApplicationContext中所有的类 -->
<dubbo:annotation package="com.foo.bar.action" />
```

## 关于 XML 配置的一些说明

也可以使用以下的 XML 配置完成 annotation 扫描，与前面的 `<dubbo:annotation package="..." />` 等价

``` xml
<dubbo:annotation />
<context:component-scan base-package="com.foo.bar.service">
    <context:include-filter type="annotation" expression="com.alibaba.dubbo.config.annotation.Service" />
</context:component-scan>
```

Spring 2.5 及以后版本支持 `<component-scan>`，对于 Spring 2.0 及以前版本，需要按照下面的方式配置：

``` xml 
<!-- Spring2.0支持@Service注解配置，但不支持package属性自动加载bean的实例，需人工定义bean的实例。-->
<dubbo:annotation />
<bean id="barService" class="com.foo.BarServiceImpl" /> 
```