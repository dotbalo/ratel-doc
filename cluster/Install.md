## 1. 安装ratel

### 1.1 安装说明

````
    集群安装配置需要两类文件: servers.yaml和集群管理的kubeconfig文件
    
    servers.yaml是ratel的配置文件, 格式如下:
        - serverName: 'xiqu'
          serverAddress: 'https://1.1.1.1:8443'
          #serverAdminUser: 'xxx'
          #serverAdminPassword: 'xxx#'
          serverAdminToken: 'null'
          serverDashboardUrl: "https://k8s.xxx.com.cn"
          production: 'false'
          kubeConfigPath: "/mnt/xxx.config"
        其中管理的方式有两种(Token暂不支持): 
            账号密码和kubeconfig形式, 只需配置一种即可, kubeconfig优先级高

    参数解析:
        serverName: 集群别名
        serverAddress: Kubernetes APIServer地址
        serverAdminUser: Kubernetes管理员账号(需要配置basic auth)
        serverAdminPassword: Kubernetes管理员密码
        serverAdminToken: Kubernetes管理员Token // 暂不支持
        serverDashboardUrl: Kubernetes官方dashboard地址
        kubeConfigPath: Kubernetes kube.config路径(绝对路径)
    kubeConfigPath 通过secret挂载到容器的/mnt目录或者其他目录
````

### 1.2 创建Secret

````
    假设配置两个集群，对应的kubeconfig是test1.config和test2.config
    ratel配置文件servers.yaml内容如下:
        - serverName: 'test1'
          serverAddress: 'https://1.1.1.1:8443'
          #serverAdminUser: 'xxx'
          #serverAdminPassword: 'xxx#'
          serverAdminToken: 'null'
          serverDashboardUrl: "https://k8s.test1.com.cn"
          production: 'false'
          kubeConfigPath: "/mnt/test1.config"
        - serverName: 'test2'
          serverAddress: 'https://1.1.1.1:8443'
          #serverAdminUser: 'xxx'
          #serverAdminPassword: 'xxx#'
          serverAdminToken: 'null'
          serverDashboardUrl: "https://k8s.test2.com.cn"
          production: 'false'
          kubeConfigPath: "/mnt/test2.config"
    创建Secret: 
        kubectl create secret generic ratel-config  --from-file=test1.config --from-file=test2.config --from-file=servers.yaml -n kube-system
````

### 1.3 部署ratel

````
    ratel的部署文件内容如下:
        apiVersion: apps/v1
        kind: Deployment
        metadata:
          labels:
            app: ratel
          name: ratel
          namespace: kube-system
        spec:
          replicas: 1
          selector:
            matchLabels:
              app: ratel
          strategy:
            rollingUpdate:
              maxSurge: 1
              maxUnavailable: 0
            type: RollingUpdate
          template:
            metadata:
              creationTimestamp: null
              labels:
                app: ratel
            spec:
              containers:
                - command:
                    - sh
                    - -c
                    - ./ratel -c /mnt/servers.yaml
                  env:
                    - name: TZ
                      value: Asia/Shanghai
                    - name: LANG
                      value: C.UTF-8
                    - name: ProRunMode
                      value: prod
                    - name: ADMIN_USERNAME
                      value: admin
                    - name: ADMIN_PASSWORD
                      value: ratel_password
                  image: dotbalo/ratel:v0.1alpha
                  imagePullPolicy: Always
                  livenessProbe:
                    failureThreshold: 2
                    initialDelaySeconds: 10
                    periodSeconds: 60
                    successThreshold: 1
                    tcpSocket:
                      port: 8888
                    timeoutSeconds: 2
                  name: ratel
                  ports:
                    - containerPort: 8888
                      name: web
                      protocol: TCP
                  readinessProbe:
                    failureThreshold: 2
                    initialDelaySeconds: 10
                    periodSeconds: 60
                    successThreshold: 1
                    tcpSocket:
                      port: 8888
                    timeoutSeconds: 2
                  resources:
                    limits:
                      cpu: 1000m
                      memory: 520Mi
                    requests:
                      cpu: 100m
                      memory: 100Mi
                  volumeMounts:
                    - mountPath: /mnt
                      name: ratel-config
              dnsPolicy: ClusterFirst
              imagePullSecrets:
                - name: myregistrykey
              restartPolicy: Always
              schedulerName: default-scheduler
              securityContext: {}
              terminationGracePeriodSeconds: 30
              volumes:
                - name: ratel-config
                  secret:
                    defaultMode: 420
                    secretName: ratel-config

    需要更改的内容如下:
        ProRunMode: 区别在于dev模式打印的是debug日志, 其他模式是info级别的日志, 实际使用时应该配置为非dev
        ADMIN_USERNAME: ratel自己的管理员账号
        ADMIN_PASSWORD: ratel自己的管理员密码
        实际使用时账号密码应满足复杂性要求,因为ratel可以直接操作所配置的资源。
        其他无需配置, 端口配置暂不支持。
````

### 1.4 Service和Ingress配置

````
    创建ratel Service的文件如下:
        apiVersion: v1
        kind: Service
        metadata:
          labels:
            app: ratel
          name: ratel
          namespace: kube-system
        spec:
          ports:
            - name: container-1-web-1
              port: 8888
              protocol: TCP
              targetPort: 8888
          selector:
            app: ratel
          type: ClusterIP

    创建ratel Ingress:
        apiVersion: extensions/v1beta1
        kind: Ingress
        metadata:
          name: ratel
          namespace: kube-system
        spec:
          rules:
          - host: krm.test.com
            http:
              paths:
              - backend:
                  serviceName: ratel
                  servicePort: 8888
                path: /
````

### 1.5 访问ratel

````
    ratel登录页如下:
    
    ratel首页如下:

    PS: 前端模板下载于网上
````