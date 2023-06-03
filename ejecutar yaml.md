Para ejecutar archivos YAML en Kubernetes, puedes utilizar el comando `kubectl apply`. A continuación, te mostraré cómo ejecutar un archivo YAML con kubectl:

1. Asegúrate de tener instalado y configurado `kubectl` en tu entorno.

2. Crea un archivo YAML con la definición del recurso que deseas crear o actualizar. Por ejemplo, puedes tener un archivo llamado `my-resource.yaml`.

3. Ejecuta el siguiente comando para aplicar el archivo YAML al clúster de Kubernetes:

```bash
kubectl apply -f my-resource.yaml
```

El comando `apply` lee el archivo YAML y crea o actualiza los recursos en el clúster según la configuración especificada en el archivo.

Si el recurso ya existe en el clúster, `apply` actualizará los campos modificados y mantendrá los valores existentes en los campos no modificados.

Si el recurso no existe, `apply` creará el recurso en el clúster.

Ten en cuenta que puedes especificar múltiples archivos YAML separados por espacios si deseas aplicar varios recursos a la vez. Por ejemplo:

```bash
kubectl apply -f my-resource1.yaml -f my-resource2.yaml
```

Así podrás ejecutar los archivos YAML en Kubernetes y crear o actualizar los recursos en tu clúster. Asegúrate de que los archivos YAML estén correctamente formateados y contengan la definición del recurso que deseas desplegar.
