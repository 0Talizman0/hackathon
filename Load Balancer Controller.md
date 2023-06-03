# Plantillas Load Balancer Controller

## Plantillas

```
apiVersion: v1
kind: Namespace
metadata:
  name: kube-system

---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: aws-load-balancer-controller
  namespace: kube-system

---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: aws-load-balancer-controller
rules:
  - apiGroups:
      - ''
    resources:
      - configmaps
      - endpoints
      - events
      - ingresses
      - ingresses/status
      - services
    verbs:
      - create
      - get
      - list
      - update
      - watch
  - apiGroups:
      - ''
    resources:
      - nodes
      - pods
      - secrets
      - services
      - namespaces
    verbs:
      - get
      - list
      - watch
  - apiGroups:
      - 'extensions'
      - 'networking.k8s.io'
    resources:
      - ingresses
    verbs:
      - get
      - list
      - watch
  - apiGroups:
      - ''
    resources:
      - events
    verbs:
      - create
      - patch

---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: aws-load-balancer-controller
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: aws-load-balancer-controller
subjects:
  - kind: ServiceAccount
    name: aws-load-balancer-controller
    namespace: kube-system

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: aws-load-balancer-controller
  namespace: kube-system
spec:
  selector:
    matchLabels:
      app.kubernetes.io/name: aws-load-balancer-controller
  replicas: 1
  template:
    metadata:
      labels:
        app.kubernetes.io/name: aws-load-balancer-controller
    spec:
      serviceAccountName: aws-load-balancer-controller
      containers:
        - name: aws-load-balancer-controller
          image: amazon/aws-load-balancer-controller:v2.4.0
          args:
            - --cluster-name=my-cluster
            - --ingress-class=alb
          env:
            - name: AWS_REGION
              value: us-west-2
          ports:
            - containerPort: 8080


```
## ejemplos reales
```
apiVersion: v1
kind: Namespace
metadata:
  name: kube-system

---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: alb-ingress-controller
  namespace: kube-system

---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: alb-ingress-controller
rules:
  - apiGroups:
      - ''
    resources:
      - configmaps
      - endpoints
      - events
      - ingresses
      - ingresses/status
      - services
    verbs:
      - create
      - get
      - list
      - update
      - watch
  - apiGroups:
      - ''
    resources:
      - nodes
      - pods
      - secrets
      - services
      - namespaces
    verbs:
      - get
      - list
      - watch
  - apiGroups:
      - 'extensions'
      - 'networking.k8s.io'
    resources:
      - ingresses
    verbs:
      - get
      - list
      - watch
  - apiGroups:
      - ''
    resources:
      - events
    verbs:
      - create
      - patch

---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: alb-ingress-controller
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: alb-ingress-controller
subjects:
  - kind: ServiceAccount
    name: alb-ingress-controller
    namespace: kube-system

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: alb-ingress-controller
  namespace: kube-system
spec:
  selector:
    matchLabels:
      app.kubernetes.io/name: alb-ingress-controller
  replicas: 1
  template:
    metadata:
      labels:
        app.kubernetes.io/name: alb-ingress-controller
    spec:
      serviceAccountName: alb-ingress-controller
      containers:
        - name: alb-ingress-controller
          image: docker.io/amazon/aws-alb-ingress-controller:v1.1.8
          args:
            - --ingress-class=alb
            - --cluster-name=my-cluster
            - --aws-vpc-id=vpc-12345678
          env:
            - name: AWS_REGION
              value: us-west-2
            - name: AWS_ACCESS_KEY_ID
              valueFrom:
                secretKeyRef:
                  name: alb-ingress-controller
                  key: access-key-id
            - name: AWS_SECRET_ACCESS_KEY
              valueFrom:
                secretKeyRef:
                  name: alb-ingress-controller
                  key: secret-access-key


```
