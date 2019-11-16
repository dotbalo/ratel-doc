## 2. 添加集群

````
    安装Ratel以后，如果需要添加集群，可以直接替换servers.yaml，等Kubernetes集群的Secret更新后，Ratel会自动更新集群配置。

    比如添加test3集群:
        之前的servers.yaml如下: 
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
        添加test3集群后如下:
            - serverName: 'test1'
              serverAddress: 'https://1.1.1.1:8443'
              #serverAdminUser: 'xxx'
              #serverAdminPassword: 'xxx#'
              serverAdminToken: 'null'
              serverDashboardUrl: "https://k8s.test1.com.cn"
              production: 'false'
              kubeConfigPath: "/mnt/test1.config"
            - serverName: 'test2'
              serverAddress: 'https://1.1.1.2:8443'
              #serverAdminUser: 'xxx'
              #serverAdminPassword: 'xxx#'
              serverAdminToken: 'null'
              serverDashboardUrl: "https://k8s.test2.com.cn"
              production: 'false'
              kubeConfigPath: "/mnt/test2.config"
            - serverName: 'test3'
              serverAddress: 'https://1.1.1.3:8443'
              #serverAdminUser: 'xxx'
              #serverAdminPassword: 'xxx#'
              serverAdminToken: 'null'
              serverDashboardUrl: "https://k8s.test3.com.cn"
              production: 'false'
              kubeConfigPath: "/mnt/test3.config"

    之后热更新原有的Secret:
        kubectl create secret generic  ratel-config --from-file=servers.yaml --from-file=test1.config --from-file=test2.config --from-file=test3.config -n kube-system --dr-run -o yaml | kubectl replace -f -

    待Kubernetes集群更新Secret后，Ratel会自动加载配置，无需重启。
````