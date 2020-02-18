## 2.5. 编辑Deployment

### 2.5.1 基本说明

````
    目前Ratel已经实现在线编辑功能，无需通过yaml文件即可完成编辑。
    目前支持的编辑项并非所有选项，其中支持编辑的选项为覆盖编辑，暂不支持的编辑项不会被覆盖。    
    编辑Deployment的Metadata页面如下：
    之后可以直接按需修改相关配置即可
````

![editdeploymentMetadata1](https://github.com/dotbalo/ratel-doc/blob/master/images/edit-deployment-metadata-1.png)
![editdeploymentMetadata2](https://github.com/dotbalo/ratel-doc/blob/master/images/edit-deployment-metadata-2.png)
![editdeploymentMetadata3](https://github.com/dotbalo/ratel-doc/blob/master/images/edit-deployment-metadata-3.png)
![editdeploymentAffinity](https://github.com/dotbalo/ratel-doc/blob/master/images/editDeploymentAffinity.png)


### 2.5.2 Volume编辑

![editVolume-1](https://github.com/dotbalo/ratel-doc/blob/master/images/edit-volume-1.png)

````
    如上图1所示，编辑Deployment、StatefulSet（storageClass暂不支持更改）或者DaemonSet时，
    Ratel会自动读取相关Volume和Projected Volume配置。
    可以进行编辑、添加或删除。
    
````

### 3.3 Container编辑

![editContainer1](https://github.com/dotbalo/ratel-doc/blob/master/images/edit-container-1.png)
![container2](https://github.com/dotbalo/ratel-doc/blob/master/images/edit-container-2.png)

````
    对于Container的在线编辑为覆盖更新，如果编辑页面没有需要更改的参数，需谨慎操作，目前支持大部分常用参数更改，
    如果没有包含你要更改的参数，不要进行更改，否则会覆盖之前的Container配置，有更改需求可以在本项目下提需求支持。
    
````

### 3.4 InitContainer编辑

````
    Init Container和Container的配置大致相同，按需添加和删除。
````

