## 3. 创建Deployment

### 3.1 Metadata配置

````
    Metadata配置页面如下(登录后单击Deployment-->创建):
````

![deploymentMetadata](https://github.com/dotbalo/ratel-doc/blob/master/images/create-deployment.png)
![deploymentMetadataKNT](https://github.com/dotbalo/ratel-doc/blob/master/images/kernel-nodeselector-taint.png)
![deploymentAffinity](https://github.com/dotbalo/ratel-doc/blob/master/images/deploymentAffinity.png)

````
    Metadata并非Deployment yaml文件中的metadata，此处放置的是一些Deployment的通用配置
    填写说明:
        选择集群: 选择之前配置的集群, 按serverName区分，选择集群后，会自动弹出Namespace的选择框。
        Namespace: 当前Deployment需要创建在哪个Namespace，Namespace的选择框支持搜索功能。
        尽量部署至不同宿主机: 此选项相当于添加了一个Pod的Affinity的软策略，基于selector实现。
        更新策略: Deployment的更新策略，此处和DaemonSet和StatefulSet更新策略不一致。
        副本数: Pod的个数，可以使用鼠标滚轮或者直接键入的方式更改。
        私有仓库Secret: 用于私有仓库镜像下载的账号密码，需要提前创建，点击刷新会自动获取集群的docker registry类型的secret。
        Labels: Labels是Deployment的label标签，当属于Deployment名字时，会自动填写一个Labels和Selector，可以按需修改、添加和删除。
        Selectors: Selectors是Pod的Labels和Deployment的Selector，按需修改、添加和删除。
        HostAliases: HostAliases是hosts文件配置，按需修改、添加和删除。

        NodeSelector: 节点选择器，按需修改、添加和删除。
        内核配置: Pod中的内核配置，如上图的第二个图，需要kubelet允许内核配置，按需修改、添加和删除。
        Taint:  如上图的第二个图，容忍配置，，按需修改、添加和删除。
        Affinity: 如上图的第三个图，亲和力配置，目前支持一键式添加、编辑节点亲和力，将容器按照规则部署至指定节点
        其他参数按需修改。

    【为了保证填入数据对的准确性和完整性，填写下一个选项时，必须单击Next，不可以直接按第一个图片的视图选项，所有的均填写完毕后可以直接点击视图选项】
````

### 3.2 Volume配置

![volume](https://github.com/dotbalo/ratel-doc/blob/master/images/volume.png)
![stsVolume](https://github.com/dotbalo/ratel-doc/blob/master/images/sts-volume.png)
![projectedVolume](https://github.com/dotbalo/ratel-doc/blob/master/images/projected-volume.png)

````
    如上图1所示，目前所支持的Volume配置有HostPath、Secret、ConfigMap、EmptyDir、PVC。
    如上图2所示，目前StatefulSet的Volume配置多了一个StorageClass配置。
    如上图3所示，Ratel支持一键式Projected类型的volume配置
    上述的Secret、ConfigMap、PVC、StorageClass无需手动输入，单击刷新后即可自动自动获取到当前集群的相关信息。
    其中StorageClass可以直接拖动如图2的申请空间大小来限制申请的动态卷的大小。
    
    另外提供了额外的Projected Volume，可以按需配置。
````

### 3.3 Container配置

![container](https://github.com/dotbalo/ratel-doc/blob/master/images/container.png)
![container2](https://github.com/dotbalo/ratel-doc/blob/master/images/container2.png)

````
    Container配置目前几乎支持所有常见配置，Container的名称会在Deployment名称键入后自动填写一个默认的，可以按需修改。
    点击如图1所示的添加按钮，可以配置多个Container，按需添加、修改和删除。
    启动命令和启动参数按需修改，三个逗号加上回车分隔（为了兼容deployment的|+ 和 |-）。
    比如：
    sh,,,
    -c,,,
    sleep 36000
    对应的deployment Command为：
    command:
    - sh
    - -c
    - sleep 36000

    集群的CPU和内存资源按需配置，直接拖动即可。

    健康检查按需配置，目前支持httpGet、tcpSocket、exec方式。

    preStop和postStart按需配置。
    
    SecurityContext按需配置。

    高权限运行是添加privilege=true参数至Container。

    容器端口按需配置和添加，目前支持三种协议配置。

    容器环境变量如图2所示，支持三种方式的容器变量配置，按需添加、修改和删除。
        字符变量: key value变量，不能留空。
        EnvFrom: 从ConfigMap和Secret中获取变量配置。
        ValueFrom: 目前支持FieldRef、ConfigMapRef、SecretRef和ResourceFieldRef配置。

    文件挂载配置:
        文件挂载配置必须先添加Volume配置，否则无法创建文件挂载。
        Volume名称自动获取创建Volume。
    
````

### 3.4 InitContainer配置

````
    Init Container和Container的配置大致相同，按需添加和删除。
````

### 3.5 Service和Ingress配置

![container-service](https://github.com/dotbalo/ratel-doc/blob/master/images/container-service.png)
![container-ingress](https://github.com/dotbalo/ratel-doc/blob/master/images/container-ingress.png)

````
    创建Deployment、DaemonSet和StatefulSet的页面，嵌入了简单的Service和Ingress配置。
    如图1所示，在配置完Container后，如果需要添加Service(默认不添加)，在开启service配置后，会根据container的端口配置自动生成Service的配置，可以按需修改、添加和删除。
    此页面Service仅支持ClusterIP和NodePort两种类型。

    如图2所示，在配置完Service后，如果需要添加Ingress(默认不添加)，在开启Ingress后，会根据Service配置默认生成一个Ingress配置，可以按需修改、添加和删除。
    如需开启https，需要提前添加tls类型的域名证书，点击刷新后即可自动读取当前集群的当前Namespace的tls类型的证书列表，无tls类型的证书无法开启https。
    去除前缀的意思是: 访问www.test1.com/a/test.html 会自动变成www.test1.com/test.html。

````

### 3.6 创建资源

````
    所有信息填写完毕后，会弹出创建按钮，点击创建即可在对于的集群的对应的namespace中创建对应的资源。
    此时可以点击不同的视图进行编辑相关信息。
    
    创建成功的页面如图:
````

![container-create-succ](https://github.com/dotbalo/ratel-doc/blob/master/images/deployment-create-succ.png)

````
    创建失败的页面如图:
    此时会打印具体的错误信息，更正后再次创建即可
````

![container-create-succ](https://github.com/dotbalo/ratel-doc/blob/master/images/deployment-create-error.png)
