dubbo 2.5.6版本新增了对netty4通信模块的支持，启用方式如下

provider端：
```xml
<dubbo:protocol server="netty4" />
```

consumer端：
```xml
<dubbo:consumer>
    <dubbo:parameter key="client" value="netty4" />
</dubbo:consumer>
```

> **注意**  
> 1. 避免provider端配置影响consumer端
> 如provider使用  
> ```xml
> <dubbo:protocol transporter="netty4" />
> ```
> 的配置形式，并且consumer端未做transporter设置，则consumer端的默认通信框架也会变为netty4。  
> 如要保持consumer端通信方式不被覆盖，请在consumer端显示配置通信框架 
> 或在provider端使用  
> ```xml
> <dubbo:protocol server="netty4" />
> ```
> 2. 以下consumer端client、transporter等配置参数当前不可用
> ```xml
> <dubbo:protocol client="netty4" transporter="netty4"/>
> ```

> 接下来我们会继续完善以下几点：
> 1. 当前两端的配置方式不对称，将在下一个版本继续完善  
> 2. 性能测试指标及与netty3版本的性能测试对比，我们会提供一份参考数据  