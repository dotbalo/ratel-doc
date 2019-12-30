## 2.5 创建Service

### 2.5.1 基本说明

````
    创建Service可以从资源列表中创建，也可以直接在创建Service的页面创建。
    目前可以将Service绑定至Deployment、StatefulSet、DaemonSet，
    选择对应的资源，可以自动生成端口列表，避免了手动创建的出错。
````

### 2.5.2 从资源列表创建Service

````
    不同资源类型创建Service的方式相同，本次以Deployment创建为例，其他资源创建类似。
````

#### 2.5.2.1 查看Deployment列表

````
    点击Deployment --> 查看，如下图所示：
````

![listDP](https://github.com/dotbalo/ratel-doc/blob/master/images/create-service-list-dp.png)

````
    点击【添加Service】按钮后如下图所示，目前仅支持ClusterIP、NodePort、None三种类型的Service，其他类型资源创建Service步骤一样
````

![createService](https://github.com/dotbalo/ratel-doc/blob/master/images/create-service.png)


### 2.5.3 直接创建Service

````
    可以直接从Service选项卡直接创建Service，点击Service --> 创建Service，如下图所示，
    可以通过选择不同的资源类型，和不同的资源进行创建，选择后对应的资源端口列表自动生成。
````

![createServiceFromService](https://github.com/dotbalo/ratel-doc/blob/master/images/create-service-from-service.png)