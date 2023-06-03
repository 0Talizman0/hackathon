¡Claro! Aquí tienes una cheatsheet básica de eksctl para ayudarte a trabajar con clústeres de Amazon EKS:

**Creación y eliminación de clústeres:**
```
# Crear un clúster de EKS
eksctl create cluster --name <nombre-cluster> --region <región> --node-type <tipo-nodo>

# Eliminar un clúster de EKS
eksctl delete cluster --name <nombre-cluster> --region <región>
```

**Administración de nodos:**
```
# Escalar el número de nodos en un grupo de nodos existente
eksctl scale nodegroup --cluster <nombre-cluster> --region <región> --name <nombre-nodo> --nodes <cantidad-nodos-deseados>

# Actualizar la configuración de un grupo de nodos existente
eksctl update nodegroup --cluster <nombre-cluster> --region <región> --name <nombre-nodo>
```

**Gestión de perfiles de Fargate:**
```
# Crear un perfil de roles de Fargate para un clúster de EKS
eksctl create fargateprofile --cluster <nombre-cluster> --region <región> --name <nombre-perfil> --namespace <namespace>

# Eliminar un perfil de roles de Fargate
eksctl delete fargateprofile --cluster <nombre-cluster> --region <región> --name <nombre-perfil>
```

**Obtener información del clúster:**
```
# Obtener información sobre los clústeres de EKS existentes
eksctl get cluster --region <región>

# Obtener información detallada sobre los nodos de un clúster
eksctl get nodegroup --cluster <nombre-cluster> --region <región>
```

Recuerda que estos son solo ejemplos básicos y puedes encontrar más opciones y funcionalidades en la documentación oficial de eksctl. Asegúrate de ajustar los comandos según tus necesidades y especificaciones del clúster de EKS que estés administrando.

¡Por supuesto! Aquí tienes más comandos para tu cheatsheet de eksctl:

**Actualización del clúster:**
```
# Actualizar la versión de Kubernetes del clúster
eksctl update cluster --name <nombre-cluster> --region <región> --kubernetes-version <versión>

# Actualizar la configuración de red del clúster
eksctl update cluster --name <nombre-cluster> --region <región> --vpc-cidr <rango-CIDR>

# Actualizar las políticas de acceso del clúster
eksctl update cluster --name <nombre-cluster> --region <región> --role-based-access-control
```

**Gestión de addons:**
```
# Instalar un addon en el clúster
eksctl utils install-<nombre-addon> --cluster <nombre-cluster> --region <región>

# Desinstalar un addon del clúster
eksctl utils uninstall-<nombre-addon> --cluster <nombre-cluster> --region <región>
```

**Gestión de logs:**
```
# Habilitar la recopilación de logs de clúster
eksctl utils update-cluster-logging --name <nombre-cluster> --region <región> --enable-types <tipos-de-logs>

# Deshabilitar la recopilación de logs de clúster
eksctl utils update-cluster-logging --name <nombre-cluster> --region <región> --disable-types <tipos-de-logs>
```

Recuerda que estos comandos son solo ejemplos y debes adaptarlos según tus necesidades específicas. La herramienta eksctl ofrece una amplia gama de funcionalidades para administrar clústeres de Amazon EKS, por lo que te recomendaría consultar la documentación oficial de eksctl para obtener más información y detalles sobre los comandos y opciones disponibles.
