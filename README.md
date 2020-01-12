## Kubernetes 一键式资源管理平台

### Ratel介绍

#### 1. Ratel是什么？
````
    Ratel是一个Kubernetes资源平台，基于管理Kubernetes的资源开发，

    可以管理Kubernetes的Deployment、DaemonSet、StatefulSet、Service、Ingress、Pods、Nodes。

    也可以管理Kubernetes的Role、ClusterRole、Rolebinding、ClusterRoleBinding、Secret、ConfigMap、PV、PVC等。

    立志于基于图形界面管理所有的Kubernetes的资源。
````

#### 2. Ratel和官方Kubernetes-Dashboard什么区别？

````
    官方的Kubernetes Dashboard可以查看Kubernetes的所有配置，包括系统资源使用情况、Pod资源使用情况
    也可以直接查看Pod的日志或者进入到Pod中执行命令。
    
    而Ratel是用于更方便创建、管理、更新Kubernetes集群中的资源，所有的资源配置都可以通过Web界面进行配置、创建，
    无需管理复杂的yaml或json文件，即可轻松实现Kubernetes的资源管理，
    同时Ratel支持多集群的图形化管理，相当于弥补了Kubernetes官方Dashboard的不足。

    比如ConfigMap创建，可以在Ratel中直接选择集群和Namespace，然后填入对应的Key和数据即可创建：
````
        
![创建ConfigMap](https://github.com/dotbalo/ratel-doc/blob/master/images/create-cm.png)

````
    也可以直接对ConfigMap进行更新:
````
        
![更新ConfigMap](https://github.com/dotbalo/ratel-doc/blob/master/images/update-cm.png)

````
    同样对集群的其他资源操作方式也是类似。
````

#### 3. Ratel的源码在哪里？

````
    Ratel采用beego开发，因为开发周期较短，目前代码比较乱，并且Ratel仍在开发中，待第一版开发完成后，并且整理完代码会放置于本项目的src目录下。
    
    PS：由于本人不太会前端开发，Ratel的前端模板基于chinaz下载的模板进行更改并开发。
````

### Ratel文档

1. 安装配置

    [1.1 Ratel安装](https://github.com/dotbalo/ratel-doc/blob/master/cluster/Install.md)
    
    [1.2 添加集群](https://github.com/dotbalo/ratel-doc/blob/master/cluster/addCluster.md)
    
2. 创建资源
    
    [2.1 创建Deployment](https://github.com/dotbalo/ratel-doc/blob/master/deployment/create-deployment.md)
    
    [2.2 创建StatefulSet](https://github.com/dotbalo/ratel-doc/blob/master/statefulset/create-statefulset.md)
    
    [2.3 创建DaemonSet](https://github.com/dotbalo/ratel-doc/blob/master/daemonset/create-daemonset.md)
    
    [2.4 创建ConfigMap](https://github.com/dotbalo/ratel-doc/blob/master/configmap/create-configmap.md)
    
    [2.5 创建Service](https://github.com/dotbalo/ratel-doc/blob/master/service/create-service.md)
    
    [2.6 创建Ingress](https://github.com/dotbalo/ratel-doc/blob/master/ingress/create-ingress.md)
    
    [2.7 创建Secret](https://github.com/dotbalo/ratel-doc/blob/master/secret/create-secret.md)
    
    [2.8 创建Namespace](https://github.com/dotbalo/ratel-doc/blob/master/namespace/create-namespace.md)
    
    
3. 编辑资源
    
    [3.1 编辑Deployment](https://github.com/dotbalo/ratel-doc/blob/master/deployment/edit-deployment.md)
    
    [3.2 编辑DaemonSet](https://github.com/dotbalo/ratel-doc/blob/master/deployment/edit-daemonset.md)
    
    [3.3 编辑StatefulSet](https://github.com/dotbalo/ratel-doc/blob/master/deployment/edit-statefulset.md)
    
    [3.4 编辑Service](https://github.com/dotbalo/ratel-doc/blob/master/service/edit-service.md)
    
    [3.5 编辑Ingress](https://github.com/dotbalo/ratel-doc/blob/master/ingress/edit-ingress.md)
    
    [3.6 资源配额管理(ResourceQuota)](https://github.com/dotbalo/ratel-doc/blob/master/namespace/create-rq.md)
    
4. 资源复制

    [4.1 资源复制](https://github.com/dotbalo/ratel-doc/blob/master/deployment/copy-resource.md)

    
#### 更多功能及文档正在完善中...
