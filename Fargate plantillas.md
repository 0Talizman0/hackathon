# hackathon plantillas Fargate

# Pod (Tarea)
```
Resources:
  MyTaskDefinition:
    Type: AWS::ECS::TaskDefinition
    Properties:
      Family: my-task-definition
      Cpu: '512'
      Memory: '1024'
      NetworkMode: awsvpc
      ExecutionRoleArn: arn:aws:iam::123456789012:role/ecsTaskExecutionRole
      ContainerDefinitions:
        - Name: my-container
          Image: nginx:latest
          PortMappings:
            - ContainerPort: 80
          LogConfiguration:
            LogDriver: awslogs
            Options:
              awslogs-group: my-log-group
              awslogs-region: us-east-1

```
## Service (Servicio):

```
Resources:
  MyService:
    Type: AWS::ECS::Service
    Properties:
      Cluster: my-cluster
      ServiceName: my-service
      TaskDefinition: !Ref MyTaskDefinition
      DesiredCount: 2
      LaunchType: FARGATE
      NetworkConfiguration:
        AwsvpcConfiguration:
          Subnets:
            - subnet-12345678
          SecurityGroups:
            - sg-12345678

```
## Deployment (Implementación):

```
Resources:
  MyDeployment:
    Type: AWS::ECS::Service
    Properties:
      Cluster: my-cluster
      ServiceName: my-deployment
      TaskDefinition: !Ref MyTaskDefinition
      DesiredCount: 2
      LaunchType: FARGATE
      NetworkConfiguration:
        AwsvpcConfiguration:
          Subnets:
            - subnet-12345678
          SecurityGroups:
            - sg-12345678
```
## ReplicaSet (Conjunto de réplicas):

```
Resources:
  MyReplicaSet:
    Type: AWS::ECS::Service
    Properties:
      Cluster: my-cluster
      ServiceName: my-replicaset
      TaskDefinition: !Ref MyTaskDefinition
      DesiredCount: 3
      LaunchType: FARGATE
      NetworkConfiguration:
        AwsvpcConfiguration:
          Subnets:
            - subnet-12345678
          SecurityGroups:
            - sg-12345678
```
## Namespace (Espacio de nombres):
AWS Fargate no utiliza el concepto de namespace de Kubernetes. En su lugar, se organiza en clústeres y grupos de servicios.

## ConfigMap
```
Resources:
  MyConfigMap:
    Type: AWS::ECS::TaskDefinition
    Properties:
      Family: my-task-definition
      Cpu: '512'
      Memory: '1024'
      NetworkMode: awsvpc
      ExecutionRoleArn: arn:aws:iam::123456789012:role/ecsTaskExecutionRole
      ContainerDefinitions:
        - Name: my-container
          Image: nginx:latest
          PortMappings:
            - ContainerPort: 80
          LogConfiguration:
            LogDriver: awslogs
            Options:
              awslogs-group: my-log-group
              awslogs-region: us-east-1
      Volumes:
        - Name: config-volume
          ConfigMap:
            Name: my-configmap

```
## Secret (Secreto)

```
Resources:
  MySecret:
    Type: AWS::ECS::TaskDefinition
    Properties:
      Family: my-task-definition
      Cpu: '512'
      Memory: '1024'
      Network

```







