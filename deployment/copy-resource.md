## 4.1 资源复制

### 4.1.1 基本说明

````
    资源复制可以一键复制Service、Deployment、StatefulSet、DaemonSet、ConfigMap至其他集群或其他Namespace中，
    复制过程可以进行自定义更改，资源复制功能使用方法类似，本次以Deployment为例。
````

### 4.1.2 选择需要的Deployment

````
    点击Deployment选项卡 --> 查看 --> 点击复制
````

![copy-select](https://github.com/dotbalo/ratel-doc/blob/master/images/copy-select.png)

````
    点击复制后的页面和创建、编辑类似，重新选择集群、Namespace后，可以直接创建资源，也可以自定义后创建。
````

![copy-deployment](https://github.com/dotbalo/ratel-doc/blob/master/images/copy-dp.png)