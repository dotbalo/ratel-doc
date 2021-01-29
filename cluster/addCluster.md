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
              harborConfig: "HarborUrl, HarborUsername, HarborPassword, HarborEmail"
            - serverName: 'test2'
              serverAddress: 'https://1.1.1.1:8443'
              #serverAdminUser: 'xxx'
              #serverAdminPassword: 'xxx#'
              serverAdminToken: 'null'
              serverDashboardUrl: "https://k8s.test2.com.cn"
              production: 'false'
              kubeConfigPath: "/mnt/test2.config"
              harborConfig: "HarborUrl, HarborUsername, HarborPassword, HarborEmail"
        添加test3集群后如下:
            - serverName: 'test1'
              serverAddress: 'https://1.1.1.1:8443'
              #serverAdminUser: 'xxx'
              #serverAdminPassword: 'xxx#'
              serverAdminToken: 'null'
              serverDashboardUrl: "https://k8s.test1.com.cn"
              production: 'false'
              kubeConfigPath: "/mnt/test1.config"
              harborConfig: "HarborUrl, HarborUsername, HarborPassword, HarborEmail"
            - serverName: 'test2'
              serverAddress: 'https://1.1.1.2:8443'
              #serverAdminUser: 'xxx'
              #serverAdminPassword: 'xxx#'
              serverAdminToken: 'null'
              serverDashboardUrl: "https://k8s.test2.com.cn"
              production: 'false'
              kubeConfigPath: "/mnt/test2.config"
              harborConfig: "HarborUrl, HarborUsername, HarborPassword, HarborEmail"
            - serverName: 'test3'
              serverAddress: 'https://1.1.1.3:8443'
              #serverAdminUser: 'xxx'
              #serverAdminPassword: 'xxx#'
              serverAdminToken: 'null'
              serverDashboardUrl: "https://k8s.test3.com.cn"
              production: 'false'
              kubeConfigPath: "/mnt/test3.config"
              harborConfig: "HarborUrl, HarborUsername, HarborPassword, HarborEmail"

    之后热更新原有的Secret:
        kubectl create secret generic  ratel-config --from-file=servers.yaml --from-file=test1.config --from-file=test2.config --from-file=test3.config -n kube-system --dr-run -o yaml | kubectl replace -f -
    
    也可以使用Ratel直接编辑该Secret

    待Kubernetes集群更新Secret后，Ratel会自动加载配置，无需重启。
````

### 2.1 添加权限控制
````
创建权限管理namespace
kubectl create ns kube-users

然后添加如下的ClusterroleBinding
vim ratel-rbac.yaml

apiVersion: v1
items:
- apiVersion: rbac.authorization.k8s.io/v1
  kind: ClusterRole
  metadata:
    annotations:
      rbac.authorization.kubernetes.io/autoupdate: "true"
    labels:
      kubernetes.io/bootstrapping: rbac-defaults
      rbac.authorization.k8s.io/aggregate-to-edit: "true"
    name: ratel-namespace-readonly
  rules:
  - apiGroups:
    - ""
    resources:
    - namespaces
    verbs:
    - get
    - list
    - watch
  - apiGroups:
    - metrics.k8s.io
    resources:
    - pods
    verbs:
    - get
    - list
    - watch
- apiVersion: rbac.authorization.k8s.io/v1
  kind: ClusterRole
  metadata:
    name: ratel-pod-delete
  rules:
  - apiGroups:
    - ""
    resources:
    - pods
    verbs:
    - get
    - list
    - delete
- apiVersion: rbac.authorization.k8s.io/v1
  kind: ClusterRole
  metadata:
    name: ratel-pod-exec
  rules:
  - apiGroups:
    - ""
    resources:
    - pods
    - pods/log
    verbs:
    - get
    - list
  - apiGroups:
    - ""
    resources:
    - pods/exec
    verbs:
    - create
- apiVersion: rbac.authorization.k8s.io/v1
  kind: ClusterRole
  metadata:
    annotations:
      rbac.authorization.kubernetes.io/autoupdate: "true"
    name: ratel-resource-edit
  rules:
  - apiGroups:
    - ""
    resources:
    - configmaps
    - persistentvolumeclaims
    - services
    - services/proxy
    verbs:
    - patch
    - update
  - apiGroups:
    - apps
    resources:
    - daemonsets
    - deployments
    - deployments/rollback
    - deployments/scale
    - statefulsets
    - statefulsets/scale
    verbs:
    - patch
    - update
  - apiGroups:
    - autoscaling
    resources:
    - horizontalpodautoscalers
    verbs:
    - patch
    - update
  - apiGroups:
    - batch
    resources:
    - cronjobs
    - jobs
    verbs:
    - patch
    - update
  - apiGroups:
    - extensions
    resources:
    - daemonsets
    - deployments
    - deployments/rollback
    - deployments/scale
    - ingresses
    verbs:
    - patch
    - update
- apiVersion: rbac.authorization.k8s.io/v1
  kind: ClusterRole
  metadata:
    name: ratel-resource-readonly
  rules:
  - apiGroups:
    - ""
    resources:
    - configmaps
    - endpoints
    - persistentvolumeclaims
    - pods
    - replicationcontrollers
    - replicationcontrollers/scale
    - serviceaccounts
    - services
    verbs:
    - get
    - list
    - watch
  - apiGroups:
    - ""
    resources:
    - bindings
    - events
    - limitranges
    - namespaces/status
    - pods/log
    - pods/status
    - replicationcontrollers/status
    - resourcequotas
    - resourcequotas/status
    verbs:
    - get
    - list
    - watch
  - apiGroups:
    - ""
    resources:
    - namespaces
    verbs:
    - get
    - list
    - watch
  - apiGroups:
    - apps
    resources:
    - controllerrevisions
    - daemonsets
    - deployments
    - deployments/scale
    - replicasets
    - replicasets/scale
    - statefulsets
    - statefulsets/scale
    verbs:
    - get
    - list
    - watch
  - apiGroups:
    - autoscaling
    resources:
    - horizontalpodautoscalers
    verbs:
    - get
    - list
    - watch
  - apiGroups:
    - batch
    resources:
    - cronjobs
    - jobs
    verbs:
    - get
    - list
    - watch
  - apiGroups:
    - extensions
    resources:
    - daemonsets
    - deployments
    - deployments/scale
    - ingresses
    - networkpolicies
    - replicasets
    - replicasets/scale
    - replicationcontrollers/scale
    verbs:
    - get
    - list
    - watch
  - apiGroups:
    - policy
    resources:
    - poddisruptionbudgets
    verbs:
    - get
    - list
    - watch
  - apiGroups:
    - networking.k8s.io
    resources:
    - networkpolicies
    verbs:
    - get
    - list
    - watch
  - apiGroups:
    - metrics.k8s.io
    resources:
    - pods
    verbs:
    - get
    - list
    - watch
kind: List
metadata:
  resourceVersion: ""
  selfLink: ""
  
kubectl create -f ratel-rbac.yaml

vim ratel-rbac-binding.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: ratel-namespace-readonly-sa
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: ratel-namespace-readonly
subjects:
- apiGroup: rbac.authorization.k8s.io
  kind: Group
  name: system:serviceaccounts:kube-users
  
  kubectl create -f ratel-rbac-binding.yaml
````
