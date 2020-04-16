## 4.2 Namespace复制

### 4.2.1 说明

````
    Ratel提供一键式复制整个Namespace，一般用于新建环境，或者跨集群迁移一个namespace的所有实例。
    目前支持几乎所有常用类型资源的复制
````

![copyNamespaceInfo](https://github.com/dotbalo/ratel-doc/blob/master/images/copy-namespace-info.png)

````
    点击对应的资源类型，可以选择迁移指定的资源或者所有资源
    
    注意: 无Selector的Service迁移后需要手动更改Endpoint的目标端口和IP
          PV和PVC的迁移需要注意正确性
````