## 2.6 创建Ingress(目前仅支持ingress nginx)

### 2.6.1 基本说明

````
    创建Ingress和创建Service类型，可以从Service列表中创建，也可以直接在创建Ingress列表中创建。
    在Service列表中选择Service创建，一个Ingress只能绑定一个Service，直接创建Ingress可以绑定同一个Namespace的多个Service。
````

### 2.6.2 从Service列表创建

````
    点击Service选项卡的查看 --> 点击添加路由，如图所示：
````

![listSvc](https://github.com/dotbalo/ratel-doc/blob/master/images/create-ingress-from-service.png)

````
    之后可以添加对应的域名绑定至service的对应端口
````

![createIngress](https://github.com/dotbalo/ratel-doc/blob/master/images/create-ingress-from-service-c.png)

````
    可以选择性的添加Ingress的注释、Labels。
    域名可以选择性添加多个域名，也可以开启HTTPS(必须添加TLS类型的secret)
    去除前缀的意思是将xxx.com/abc/1 代理到 xxx.com/1(开启去除前缀后，会创建一个名称为xxx-strip-path的ingress，和不去除前缀的ingress分开)
````

### 2.6.3 直接创建Ingress

````
    相对于上一个创建方式，直接创建Ingress可以绑定多个Service，点击Ingress选项卡 --> 创建，如下图所示
````

![createIngress](https://github.com/dotbalo/ratel-doc/blob/master/images/create-ingress.png)

````
    选择对应的Kubernetes集群、Namespace和Service(多选)，之后可以生成对应的ingress列表，配置方式和上述方式一致，如图
````


