## 5.1 账号管理

### 5.1.1 基于Basic账号管理

````
    参考链接：https://www.cnblogs.com/dukuan/p/11976406.html
````

### 5.1.2 基于ServiceAccount

````
    基于ServiceAccount是推荐的账号管理方式，为了方便开发及测试登录k8s的Dashboard，进行相关操作，目前仅支持如下权限配置
````

![serviceAccountPer](https://github.com/dotbalo/ratel-doc/blob/master/images/serviceAccountPer.png)

````
    和基本认证区别是需要提前创建名为kube-users的namespace
    然后添加如下的ClusterroleBinding
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
---
apiVersion: rbac.authorization.k8s.io/v1
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
````