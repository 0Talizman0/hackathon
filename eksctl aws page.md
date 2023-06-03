Aquí tienes un ejemplo de cómo utilizar eksctl para crear un clúster de Amazon EKS y desplegar un servicio web utilizando NGINX:

1. Crea un archivo YAML llamado `cluster.yaml` con la configuración del clúster de EKS:

```yaml
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig
metadata:
  name: my-cluster
  region: us-west-2
nodeGroups:
  - name: ng-1
    instanceType: t3.medium
    desiredCapacity: 2
    privateNetworking: true
    iam:
      withAddonPolicies:
        externalDNS: true
```

2. Crea un archivo YAML llamado `nginx.yaml` con la configuración del despliegue y el servicio de NGINX:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:latest
          ports:
            - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer
```

3. Ejecuta el siguiente comando para crear el clúster de EKS:

```bash
eksctl create cluster -f cluster.yaml
```

Esto creará un clúster de EKS con el nombre `my-cluster` en la región `us-west-2`, y también creará un grupo de nodos con 2 instancias EC2 de tipo `t3.medium`.

4. Ejecuta el siguiente comando para aplicar la configuración de NGINX al clúster:

```bash
kubectl apply -f nginx.yaml
```

Esto creará un Deployment con 2 réplicas de la imagen de NGINX y un Service de tipo LoadBalancer para exponer el servicio.

Puedes acceder a la página web a través de la URL proporcionada por el balanceador de carga. Asegúrate de configurar correctamente el balanceador de carga y de que los puertos y etiquetas coincidan con los especificados en el archivo YAML.

Recuerda adaptar los archivos YAML según tus necesidades específicas, como el nombre del clúster, la región, el tipo de instancia, el número de réplicas y la versión de la imagen de NGINX que deseas utilizar.
