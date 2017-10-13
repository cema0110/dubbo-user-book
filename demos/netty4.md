dubbo 2.5.6版本新增了对netty4通信模块的支持，启用方式如下

provider端：
```xml
<dubbo:protocol transporter="netty4" />
```
或
```xml
<dubbo:protocol server="netty4" />
```

consumer端：
```xml
<dubbo:protocol transporter="netty4" />
```

> **注意**  
> provider使用  
> ```xml
> <dubbo:protocol transporter="netty4" />
> ```
> 的配置形式，如果consumer端未做transporter设置，则consumer端的默认通信方式也会变为netty4。  
> 如要保持consumer端通信方式不被覆盖，请在consumer端显示设置  
> ```xml
> <dubbo:protocol transporter="netty4" />
> ``` 
> 或在provider端使用  
> ```xml
> <dubbo:protocol server="netty4" />
> ```

> 接下来我们会继续完善以下几点：
> 1. 配置方式在下一个版本会继续完善  
> 2. 性能测试指标及与netty3版本的性能测试对比，我们会提供一份参考数据  