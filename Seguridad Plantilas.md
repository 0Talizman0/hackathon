# Plantillas seguras con la metodologia shift-left

## Pod (Punto de orquestación de contenedores):
```
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: my-container
      image: nginx:1.21.1
      ports:
        - containerPort: 80
      securityContext:
        runAsNonRoot: true
        allowPrivilegeEscalation: false
        readOnlyRootFilesystem: true
      livenessProbe:
        httpGet:
          path: /healthz
          port: 80
        initialDelaySeconds: 10
        periodSeconds: 10
      readinessProbe:
        httpGet:
          path: /healthz
          port: 80
        initialDelaySeconds: 5
        periodSeconds: 10

```
En este ejemplo, se aplican las siguientes prácticas de seguridad Shift-Left:

Se utiliza una imagen oficial y específica de nginx con la etiqueta 1.21.1 para evitar versiones vulnerables.
Se define un contexto de seguridad ('securityContext') para el contenedor que restringe los privilegios, evita la escalada de privilegios y establece el sistema de archivos raíz en solo lectura.
Se configuran sondas de estado ('livenessProbe' y 'readinessProbe') para garantizar que el contenedor esté en un estado saludable antes de enviar tráfico a él.

## Service (Servicio):
Aquí tienes un ejemplo seguro de un Service en Kubernetes siguiendo la metodología Shift-Left:

```
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  type: ClusterIP

```
En este ejemplo, se aplican las siguientes prácticas de seguridad Shift-Left:

Se define el tipo de servicio como ClusterIP, lo que limita el acceso desde fuera del clúster y mantiene el servicio accesible internamente.
Se especifica un puerto de destino (targetPort) que corresponde al puerto en el que el contenedor del pod está escuchando internamente.
Se utiliza el protocolo TCP para la comunicación.

## Deployment (Implementación):
Este es un ejemplo seguro de un Deployment en Kubernetes siguiendo la metodología Shift-Left:

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-container
          image: nginx:1.21.1
          ports:
            - containerPort: 80
          securityContext:
            runAsNonRoot: true
            allowPrivilegeEscalation: false
            readOnlyRootFilesystem: true
          livenessProbe:
            httpGet:
              path: /healthz
              port: 80
            initialDelaySeconds: 10
            periodSeconds: 10
          readinessProbe:
            httpGet:
              path: /healthz
              port: 80
            initialDelaySeconds: 5
            periodSeconds: 10

```
En este ejemplo, se aplican las mismas prácticas de seguridad Shift-Left que en el caso del Pod, pero esta vez se definen tres réplicas del Pod para garantizar alta disponibilidad y tolerancia a fallos.

## ReplicaSet (Conjunto de réplicas):
Aquí tienes un ejemplo seguro de un ReplicaSet en Kubernetes siguiendo la metodología Shift-Left:

```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-container
          image: nginx:1.21.1
          ports:
            - containerPort: 80
          securityContext:
            runAsNonRoot: true
            allowPrivilegeEscalation: false
            readOnlyRootFilesystem: true
          livenessProbe:
            httpGet:
              path: /healthz
              port: 80
            initialDelaySeconds: 10
            periodSeconds: 10
          readinessProbe:
            httpGet:
              path: /healthz
              port: 80
            initialDelaySeconds: 5
            periodSeconds: 10

```
