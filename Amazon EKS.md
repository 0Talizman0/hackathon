# Plantillas Amazon EKS

## Cluster (Clúster):
```
Resources:
  MyCluster:
    Type: AWS::EKS::Cluster
    Properties:
      Name: my-cluster
      RoleArn: arn:aws:iam::123456789012:role/eks-cluster-role
      ResourcesVpcConfig:
        SubnetIds:
          - subnet-12345678
          - subnet-23456789
        SecurityGroupIds:
          - sg-12345678
          - sg-23456789
      Version: "1.21"

```
## NodeGroup (Grupo de nodos):
```
Resources:
  MyNodeGroup:
    Type: AWS::EKS::Nodegroup
    Properties:
      ClusterName: my-cluster
      NodegroupName: my-nodegroup
      NodeRole: arn:aws:iam::123456789012:role/eks-nodegroup-role
      Subnets:
        - subnet-12345678
        - subnet-23456789
      ScalingConfig:
        MinSize: 1
        MaxSize: 5
        DesiredSize: 2

```

## Service Account (Cuenta de servicio):
```
Resources:
  MyServiceAccount:
    Type: AWS::IAM::Role
    Properties:
      RoleName: my-service-account
      AssumeRolePolicyDocument:
        Version: 2012-10-17
        Statement:
          - Effect: Allow
            Principal:
              Service: eks.amazonaws.com
            Action: sts:AssumeRole
      ManagedPolicyArns:
        - arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess

```
## Ingress (Ingreso):

```
Resources:
  MyIngress:
    Type: AWS::ElasticLoadBalancingV2::Ingress
    Properties:
      Name: my-ingress
      IngressClassName: alb
      Rules:
        - Priority: 1
          Host: mydomain.com
          Path: /
          Backend:
            ServiceName: my-service
            ServicePort: 80

```
## Namespace (Espacio de nombres):

```
Resources:
  MyNamespace:
    Type: AWS::EKS::Namespace
    Properties:
      Name: my-namespace
      ClusterName: my-cluster

```
## Service (Servicio):
```
Resources:
  MyService:
    Type: AWS::EKS::Service
    Properties:
      Name: my-service
      ClusterName: my-cluster
      Namespace: default
      ServiceType: LoadBalancer
      LoadBalancerIp: 10.0.0.1
      Ports:
        - Port: 80
          TargetPort: 8080
      Selector:
        app: my-app

```
## Deployment (Implementación):
```
Resources:
  MyDeployment:
    Type: AWS::EKS::Deployment
    Properties:
      Name: my-deployment
      ClusterName: my-cluster
      Namespace: default
      Replicas: 3
      RevisionTemplate:
        Spec:
          Template:
            Metadata:
              Labels:
                app: my-app
            Spec:
              Containers:
                - Name: my-container
                  Image: nginx:latest
                  PortMappings:
                    - ContainerPort: 80

```
## ConfigMap:
```
Resources:
  MyConfigMap:
    Type: AWS::EKS::ConfigMap
    Properties:
      Name: my-configmap
      ClusterName: my-cluster
      Namespace: default
      Data:
        key1: value1
        key2: value2

```
## Secret (Secreto):
```
Resources:
  MySecret:
    Type: AWS::EKS::Secret
    Properties:
      Name: my-secret
      ClusterName: my-cluster
      Namespace: default
      Data:
        username: BASE64_ENCODED_USERNAME
        password: BASE64_ENCODED_PASSWORD

```
































































