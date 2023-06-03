Aquí tienes un paso a paso para levantar un clúster de Amazon Elastic Kubernetes Service (EKS) y los nodos utilizando la línea de comandos:

1. Configuración inicial:
   - Instala y configura la CLI de AWS siguiendo la documentación oficial de AWS.
   - Configura tus credenciales de AWS ejecutando `aws configure` y proporcionando tu Access Key ID, Secret Access Key, región preferida y formato de salida.

2. Creación del clúster EKS:
   - Crea un clúster de EKS ejecutando el siguiente comando:
     ```
     eksctl create cluster --name <nombre-cluster> --region <región>
     ```
   - Espera unos minutos hasta que se complete la creación del clúster. Puedes verificar el estado del clúster ejecutando:
     ```
     eksctl get cluster --region <región>
     ```

3. Configuración de la línea de comandos de Kubernetes:
   - Configura tu entorno local para interactuar con el clúster EKS mediante el siguiente comando:
     ```
     aws eks --region <región> update-kubeconfig --name <nombre-cluster>
     ```
   - Verifica que la configuración se haya realizado correctamente ejecutando:
     ```
     kubectl config current-context
     ```

4. Creación de nodos:
   - EKS utiliza nodos administrados por AWS Fargate o nodos gestionados por el usuario mediante EC2. A continuación, se detalla la creación de nodos con Fargate:
     - Crea un perfil de roles para Fargate ejecutando el siguiente comando:
       ```
       eksctl create fargateprofile --cluster <nombre-cluster> --region <región> --name <nombre-fargate-profile>
       ```
     - Espera unos minutos hasta que se complete la creación del perfil de roles.
   - Si deseas utilizar nodos gestionados por EC2 en lugar de Fargate, debes seguir la documentación oficial de AWS para crear y configurar los nodos EC2.

Una vez que hayas completado estos pasos, tendrás un clúster de EKS listo para ejecutar tus aplicaciones en Kubernetes. Puedes utilizar comandos como `kubectl get nodes` para verificar que los nodos estén en estado "Ready" y comenzar a desplegar tus recursos en el clúster.

Recuerda que estos son solo pasos generales y pueden requerir ajustes según tus necesidades y preferencias específicas. Consulta la documentación oficial de AWS para obtener información más detallada y actualizada sobre la creación y configuración de clústeres de EKS.
