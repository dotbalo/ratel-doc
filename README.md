# 注意：该项目已不再维护，新版Kubernetes多集群资源平台已经在重构中

新版地址：https://github.com/dotbalo/krm

# 超全面、超详细的Kubernetes视频教程，基于最新K8s进行讲解
# 课程具备完善的售后服务，免费更新、免费技术问答、免费岗位推荐
https://ke.qq.com/course/2738602

咨询QQ727585266

# 注意
````
  之前的版本写command和args的时候，格式为： sh,,,-c,,,sleep 36000
  新版写法为：
  sh,,,
  -c,,,
  sleep 36000
  也就是把换行从,,,改成了,,, + 回车，为了兼容deployment的|+ 和 |-
  对应的deployment Command为：
  command:
  - sh
  - -c
  - sleep 36000
````

## Kubernetes 一键式资源管理平台

### Ratel介绍

#### 1. Ratel是什么？
````
    Ratel是一个Kubernetes多集群资源管理平台，基于管理Kubernetes的资源开发，

    可以管理Kubernetes的Deployment、DaemonSet、StatefulSet、Service、Ingress、Pods、Nodes、CronJob等。

    也可以管理Kubernetes的Role、ClusterRole、Rolebinding、ClusterRoleBinding、Secret、ConfigMap、PV、PVC等。

    立志于基于图形界面管理所有的Kubernetes的资源。
    
    同时具备了一些常用的功能，比如跨集群资源复制、一键项目迁移、图形化资源编辑、资源一键回滚及更新、一键式用户权限管理等，
    
    并且具备K8s不具备的功能，比如ConfigMap和Secret备份功能。
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
    
    [2.4 创建和编辑ConfigMap](https://github.com/dotbalo/ratel-doc/blob/master/configmap/create-configmap.md)
    
    [2.5 创建Service](https://github.com/dotbalo/ratel-doc/blob/master/service/create-service.md)
    
    [2.6 创建Ingress](https://github.com/dotbalo/ratel-doc/blob/master/ingress/create-ingress.md)
    
    [2.7 创建和编辑Secret](https://github.com/dotbalo/ratel-doc/blob/master/secret/create-secret.md)
    
    [2.8 创建Namespace](https://github.com/dotbalo/ratel-doc/blob/master/namespace/create-namespace.md)
    
    [2.9 创建pv和pvc](https://github.com/dotbalo/ratel-doc/blob/master/pvpvc/create-pvpvc.md)
    
    
3. 编辑资源
    
    [3.1 编辑Deployment](https://github.com/dotbalo/ratel-doc/blob/master/deployment/edit-deployment.md)
    
    [3.2 编辑DaemonSet](https://github.com/dotbalo/ratel-doc/blob/master/deployment/edit-daemonset.md)
    
    [3.3 编辑StatefulSet](https://github.com/dotbalo/ratel-doc/blob/master/deployment/edit-statefulset.md)
    
    [3.4 编辑Service](https://github.com/dotbalo/ratel-doc/blob/master/service/edit-service.md)
    
    [3.5 编辑Ingress](https://github.com/dotbalo/ratel-doc/blob/master/ingress/edit-ingress.md)
    
    [3.6 资源配额管理(ResourceQuota)](https://github.com/dotbalo/ratel-doc/blob/master/namespace/create-rq.md)
    
4. 资源复制

    [4.1 资源复制](https://github.com/dotbalo/ratel-doc/blob/master/deployment/copy-resource.md)

    [4.2 Namespace复制](https://github.com/dotbalo/ratel-doc/blob/master/namespace/copy-resource.md)
    
5. 账号管理
    
    [5.1 账号管理](https://github.com/dotbalo/ratel-doc/blob/master/users/users.md)
    
#### 更多功能及文档正在完善中...

