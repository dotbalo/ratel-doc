## 4. 创建StatefulSet

### 4.1 Metadata配置

````
    Metadata配置和Deployment大致相同，主要是StatefulSet的更新策略有所变化，更新策略有RollingUpdate和OnDelete两种，
    并且RollingUpdate采用的是Partition
    如下图所示:
````

![create-sts-metadata](https://github.com/dotbalo/ratel-doc/blob/master/images/create-sts-metadata.png)

![create-sts-metadata-2](https://github.com/dotbalo/ratel-doc/blob/master/images/create-sts-metadata-ru.png)


### 4.2 Volume配置

````
    Volume配置和Deployment的Volume配置也大致相同，区别在于StatefulSet多了一个StorageClass类型的Volume，如图所示:
````

![create-sts-volume-sc](https://github.com/dotbalo/ratel-doc/blob/master/images/sts-volume-sc.png)

### 4.3 Container和InitContainer

````
    Container和InitContainer配置和Deployment相同
````

### 4.4 Service配置

````
    Service配置比Deployment多了一个使用先有Service配置，点击刷新即可获取当前集群当前namespace的Service列表，
    也可以创建新的Service，创建StatefulSet必须有Service，如下图所示:
````

![create-sts-svc](https://github.com/dotbalo/ratel-doc/blob/master/images/sts-service.png)