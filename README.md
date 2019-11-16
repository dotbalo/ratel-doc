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
    
    而Ratel是用于更方便创建、管理、更新Kubernetes集群中的资源，所有的资源配置都可以通过Web通知台进行配置、创建，无需管理复杂的yaml或json文件，接口轻松实现Kubernetes的资源管理，
    同时Ratel支持多集群的图形化管理，相当于弥补了Kubernetes官方Dashboard的不足。

    比如ConfigMap创建，可以在Ratel中直接选择集群和Namespace，然后填入对应的Key和数据即可创建：
        
    ConfigMap更新

````
