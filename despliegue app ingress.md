Aquí tienes un ejemplo de cómo desplegar una aplicación con un recurso Ingress en Kubernetes:

1. Crea un archivo YAML llamado `myapp-deployment.yaml` con el siguiente contenido:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
        - name: myapp-container
          image: myapp:latest
          ports:
            - containerPort: 80
```

2. Crea un archivo YAML llamado `myapp-service.yaml` con el siguiente contenido:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: ClusterIP
```

3. Crea un archivo YAML llamado `myapp-ingress.yaml` con el siguiente contenido:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: myapp-ingress
spec:
  rules:
    - host: myapp.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: myapp-service
                port:
                  number: 80
```

4. Aplica los archivos YAML al clúster de Kubernetes:

```bash
kubectl apply -f myapp-deployment.yaml
kubectl apply -f myapp-service.yaml
kubectl apply -f myapp-ingress.yaml
```

Esto creará un Deployment con dos réplicas de la aplicación, un Service para exponer la aplicación internamente y un Ingress para enrutar el tráfico externo a la aplicación en función del nombre de host `myapp.example.com`.

Recuerda adaptar los archivos YAML según las necesidades específicas de tu aplicación, como la imagen, los puertos y el nombre de host. Además, asegúrate de tener un controlador de Ingress configurado en tu clúster de Kubernetes para que el recurso Ingress funcione correctamente.
