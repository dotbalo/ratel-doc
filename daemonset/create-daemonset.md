## 5. 创建DaemonSet

### 5.1 Metadata配置

````
    Metadata配置和Deployment大致相同，主要是DaemonSet的更新策略有所变化，更新策略有RollingUpdate和OnDelete两种，
    并且RollingUpdate没有maxSurge参数，如下图1所示。

    DaemonSet没有replicas参数

````

![create-ds-ru](https://github.com/dotbalo/ratel-doc/blob/master/images/daemonset-ru.png)


### 5.2 其他配置

````
    DaemonSet其他配合和Deployment相同
````
