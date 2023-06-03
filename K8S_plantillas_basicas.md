# Hackathon Plantillas

## Pod

Un Pod es la unidad básica de ejecución en Kubernetes. Representa uno o más contenedores que se ejecutan juntos en un mismo nodo y comparten el mismo espacio de red y recursos. Los Pods son efímeros y pueden ser creados, eliminados o reemplazados por Kubernetes según sea necesario.

```
apiVersion: v1
kind: Pod
metadata:
  name: nombre-del-pod
spec:
  containers:
  - name: nombre-del-contenedor
    image: nombre-de-la-imagen:tag
    ports:
    - containerPort: puerto-del-contenedor
```
### ejemplo real
```
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
    - name: nginx-container
      image: nginx:latest
      ports:
        - containerPort: 80

```
## Cluster
Un clúster en el contexto de Kubernetes es un conjunto de nodos (máquinas) que trabajan juntos para ejecutar y administrar aplicaciones en contenedores. Un clúster de Kubernetes es la base fundamental de la plataforma y proporciona un entorno para ejecutar, escalar y administrar aplicaciones distribuidas.

En un clúster de Kubernetes, hay dos tipos principales de nodos:

Nodos de control (Control Plane): Son responsables de gestionar y coordinar las operaciones del clúster. Estos nodos ejecutan componentes centrales de Kubernetes, como el planificador (scheduler), el controlador de replicación (replication controller) y el API Server, que proporciona la interfaz para administrar el clúster.

Nodos de trabajo (Worker Nodes): Son los nodos donde se ejecutan los contenedores que forman las aplicaciones. Estos nodos están a cargo de ejecutar los contenedores y proporcionar los recursos necesarios para su funcionamiento, como CPU, memoria y almacenamiento.

```
apiVersion: kind.x-k8s.io/v1alpha4
kind: Cluster
nodes:
- role: control-plane
- role: worker

```
### ejemplo real
```
apiVersion: kind.x-k8s.io/v1alpha4
kind: Cluster
nodes:
- role: control-plane
- role: worker
- role: worker

```

## Service
Un Service en Kubernetes es una abstracción que define un conjunto lógico de Pods y una política de acceso a ellos. Proporciona una dirección IP estable y un nombre de DNS para que otros recursos dentro o fuera del clúster puedan acceder a los Pods de forma confiable.

```
apiVersion: v1
kind: Service
metadata:
  name: nombre-del-servicio
spec:
  selector:
    app: nombre-del-deployment
  ports:
  - protocol: TCP
    port: puerto-de-servicio
    targetPort: puerto-del-contenedor

```
### ejemplo real
```
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

## Deployment
Un Deployment se utiliza para administrar la creación y actualización de Pods en Kubernetes. Proporciona declarativamente un mecanismo para garantizar un número especificado de réplicas de Pods en ejecución y permite realizar actualizaciones controladas del conjunto de Pods.

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nombre-del-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nombre-del-deployment
  template:
    metadata:
      labels:
        app: nombre-del-deployment
    spec:
      containers:
      - name: nombre-del-contenedor
        image: nombre-de-la-imagen:tag
        ports:
        - containerPort: puerto-del-contenedor

```
### ejemplo real
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-app
  template:
    metadata:
      labels:
        app: nginx-app
    spec:
      containers:
        - name: nginx-container
          image: nginx:latest
          ports:
            - containerPort: 80
```

## ReplicaSet
Un ReplicaSet garantiza que un número específico de réplicas de un Pod esté en ejecución en todo momento. Cuando se utiliza un Deployment para administrar los Pods, en realidad se crea un ReplicaSet en segundo plano para asegurar que se cumpla el número 

```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nombre-del-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nombre-del-replicaset
  template:
    metadata:
      labels:
        app: nombre-del-replicaset
    spec:
      containers:
      - name: nombre-del-contenedor
        image: nombre-de-la-imagen:tag
        ports:
        - containerPort: puerto-del-contenedor


```
### ejemplo real
```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-app
  template:
    metadata:
      labels:
        app: nginx-app
    spec:
      containers:
        - name: nginx-container
          image: nginx:latest
          ports:
            - containerPort: 80
```

## Namespace
Un Namespace en Kubernetes es un mecanismo para proporcionar aislamiento y separación lógica dentro de un clúster. Permite dividir el clúster en múltiples espacios virtuales, lo que ayuda a organizar y gestionar los recursos de manera más efectiva.
```
apiVersion: v1
kind: Namespace
metadata:
  name: nombre-del-namespace

```
### ejemplo real
```
apiVersion: v1
kind: Namespace
metadata:
  name: my-namespace
```
## ConfigMap
Un ConfigMap se utiliza para almacenar datos de configuración no confidenciales en pares clave-valor. Permite que los contenedores accedan a la configuración de la aplicación sin tener que codificarla dentro de las imágenes de los contenedores, lo que facilita la gestión y la configuración flexible.

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-configmap
data:
  app_config: |
    key1: value1
    key2: value2

```
### ejemplo real
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-configmap
data:
  database_url: jdbc:mysql://localhost:3306/mydatabase
  api_key: abcdef1234567890

```
## Secret


```
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  username: BASE64_ENCODED_USERNAME
  password: BASE64_ENCODED_PASSWORD

```
### ejemplo real
```
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  username: YWRtaW4=   # Base64 encoded value for "admin"
  password: MWYyZDFlMmU2N2Rm    # Base64 encoded value for "1f2d1e2e67df"

```



```








