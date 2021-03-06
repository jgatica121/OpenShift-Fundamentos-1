# Descripción general de la arquitectura

### Temas del módulo
* Visión general
* Proveedores de productos e infraestructura
* Arquitectura y conceptos
* Operadores
* Flujo de trabajo de redes
* Flujo de trabajo de implementación de contenedores

#### Red Hat ® OpenShift ® Plataforma de contenedores
* Plataforma de orquestación de contenedores basada en Kubernetes
* Beneficia tanto a las operaciones como al desarrollo
* Proporciona a los desarrolladores y organizaciones de TI una plataforma de aplicaciones en la nube
* Se utiliza para implementar aplicaciones en recursos seguros y escalables.
* Gastos generales mínimos de configuración y administración
* Admite Java ™, Python, Ruby, Node.js, Perl, PHP, .NET y más
* Construido sobre Kubernetes
* El plano de control de OpenShift Container Platform solo está disponible para su implementación en RHCOS
* Las cargas de trabajo de OpenShift Container Platform se pueden implementar en RHCOS o Red Hat Enterprise Linux® (RHEL)
* RHCOS disponible solo para implementaciones de OpenShift, no para uso general
* RHCOS codifica la experiencia operativa para OpenShift con nuevas herramientas especialmente diseñadas
* RHCOS es compatible con FIPS
* Lleva la plataforma Kubernetes a los centros de datos de los clientes y a la nube
* Cumple con los requisitos de seguridad, privacidad, cumplimiento y gobernanza

### Visión general
![Alt text](Imagenes/Diagrama_Alto_Nivel_OpenShift.png?raw=true "Arquitectura de alto nivel de OpenShift")


## Proveedores de productos e infraestructura
### Infraestructuras soportadas
* OpenShift compatible con RHCOS y RHEL
* Solución de nube híbrida OpenShift 4
* Compatible con nubes públicas y privadas, así como sin sistema operativo
* La automatización completa (IPI) es compatible con:
  * AWS, Microsoft Azure, Google Cloud Platform
  * Red Hat Virtualization, Red Hat OpenStack ® Platform
* Infraestructura preexistente (UPI) compatible con:
  * AWS, Microsoft Azure, Google Cloud Platform
  * VMware vSphere, Red Hat OpenStack Platform, IBM Z
  * IBM Power Systems, bare metal
* Versiones futuras para admitir aún más infraestructuras

![Alt text](Imagenes/Infraestructuras-soportadas.png?raw=true "Infraestructuras soportadas")

**OpenShift es capaz de automatizar la implementación de infraestructura y la implementación de productos. Esto también se conoce como Infraestructura aprovisionada por el instalador o IPI.**

**OpenShift también es compatible para la instalación en una infraestructura preexistente, en la que el cliente ha configurado de antemano networking,compute, y storage. Esto se conoce como infraestructura aprovisionada por el usuario o UPI.**

#### Proveedores de productos e infraestructura
##### OpenShift 3.11
* Compatible en cualquier lugar donde se ejecute RHEL
* Máquinas físicas completas, infraestructura virtualizada, en nubes privadas o públicas certificadas
* Plataformas de virtualización: Red Hat Virtualization, vSphere, Hyper-V
* Red Hat OpenStack Platform, proveedores de nube pública certificados como Amazon, Google, Azure
* Arquitecturas de servidor x86 e IBM Power

##### OpenShift Kubernetes Engine
* Los usuarios exploran OpenShift 4 Kubernetes Engine, no toda la plataforma
* Funcionalidad básica de Kubernetes con un gran ecosistema de ISV
* Disfrute de la arquitectura inmutable y segura de RHCOS
* Appeals to DIY, *KS, or lower end

## Arquitectura y conceptos
### Host de nodo
* OpenShift se ejecuta en RHCOS y RHEL
* OpenShift tiene dos tipos de nodos:
  * Workers
  * Masters
* Los nodos son:
  * Instancias de RHEL o RHCOS con OpenShift instalado
  * Workers: donde se ejecutan las aplicaciones de usuario final
  * Masters: administrar el clúster

### Contenedores
* Las instancias y componentes de la aplicación se ejecutan en contenedores compatibles con OCI
* Images: Aplicación "binaria"
* Containers: Runtime
* El nodo trabajador de OpenShift puede ejecutar muchos contenedores
* Capacidad de nodo relacionada con la memoria y las capacidades de la CPU de los recursos subyacentes
  * Nube, hardware o virtualizado
  
**La capacidad de un nodo Workers está relacionada con las capacidades de memoria y CPU de los recursos subyacentes, ya sea en la nube, en hardware o virtualizados.**

### POD
* Uno o más contenedores implementados juntos en un host
  * Consiste en un grupo de contenedores colocados con recursos compartidos como volúmenes y direcciones IP
  * La unidad de cómputo más pequeña definida, implementada y administrada
* Puede contener una o más aplicaciones colocadas estrechamente acopladas, que se ejecutan con contexto compartido
  * Ejemplo: servidor web y aplicación para extraer y sincronizar archivos
  * Modela el host lógico específico de la aplicación en un entorno en contenedor
  * En el mundo anterior al contenedor, las aplicaciones se ejecutan en el mismo host físico o virtual
  * En OpenShift, los pods reemplazan los contenedores de aplicaciones individuales como la unidad desplegable más pequeña
  
 ### POD 
* Unidad orquestada en OpenShift
  * OpenShift programa y ejecuta todos los contenedores en pod en el mismo nodo
* Aplicaciones complejas compuestas por muchos pods, cada uno con sus propios contenedores
  * Interactuar externamente y también entre sí dentro del entorno OpenShift
* OpenShift ejecuta imágenes de contenedor en contenedores envueltos por un meta objeto llamado "pod"
* Es posible tener varios contenedores en un solo pod
  * Ejemplo: para admitir funciones de clúster como contenedores sidecar
* La mayoría de las aplicaciones se benefician de la flexibilidad de la cápsula de un solo contenedor
 * Los diferentes componentes, como el servidor de aplicaciones y la base de datos, generalmente no se colocan en un solo pod
 * Permite que los componentes individuales de la aplicación se escalen fácilmente horizontalmente
* Los componentes de la aplicación están conectados por servicios

**OpenShift puede consumir la mayoría de las imágenes de contenedores que cumplen con OCI. OpenShift ejecuta imágenes en contenedores envueltos por el meta objeto llamado pod.**

### POD

* Úselo **oc get pod** para ver los pods que se ejecutan en el entorno, generalmente su proyecto:
  * Proyectos también llamados namespaces
  * Algunos pods se ejecutan hasta su finalización, como los constructores y los implementadores
  * Algunos pods continúan ejecutando la aplicación
  
  ![Alt text](Imagenes/OC-GET-PODS.png?raw=true "Arquitectura de alto nivel de OpenShift")

### Servicio
* Define un conjunto lógico de pods y una política de acceso.
  * Proporciona una dirección IP interna permanente y un nombre de host para que otras aplicaciones utilicen mientras se crean y destruyen los pods
*La capa de servicio conecta los componentes de la aplicación juntos
  * Ejemplo: el servicio web front-end se conecta a la instancia de la base de datos comunicándose con su servicio
* Los servicios permiten un equilibrio de carga interno simple entre los componentes de la aplicación
  * OpenShift inyecta automáticamente información de servicio en contenedores en ejecución para facilitar el descubrimiento
  
**Un recurso de servicio es una abstracción que define un conjunto lógico de pods y una política que se utiliza para acceder a los pods.**

**Cuando se crean o destruyen pods al escalar hacia arriba o hacia abajo, una dirección IP permanente o un nombre de host debe estar disponible para que otras aplicaciones se conecten. Un servicio representa un grupo de pods y proporciona la dirección IP permanente y el nombre de host para que lo utilicen otras aplicaciones.**

### Etiquetas
* Se utiliza para organizar, agrupar o seleccionar objetos API.
  * Ejemplo: etiquetar pods con etiquetas, los servicios utilizan selectores de etiquetas para identificar los pods a los que sirven como proxy
  * Hace posible que los servicios hagan referencia a grupos de pods
  * Capaz de tratar pods con contenedores potencialmente diferentes como entidades relacionadas
* La mayoría de los objetos pueden incluir etiquetas en metadatos.
* Agrupar objetos relacionados arbitrariamente con etiquetas
  * Ejemplo: todos los pods, servicios, controladores de replicación y configuraciones de implementación de la aplicación
* Las etiquetas son pares clave-valor simples:
  
![Alt text](Imagenes/Etiquetas.png?raw=true "Arquitectura de alto nivel de OpenShift")

**Las etiquetas se utilizan para organizar, agrupar o seleccionar objetos de API. Por ejemplo, puede etiquetar pods con etiquetas para que los servicios puedan usar selectores de etiquetas para identificar a qué pods utilizar como proxy.**

### Nodos Masters
* Instancias de RHCOS
* Funciones primarias:
  * Organice actividades en los nodos trabajadores
  * Conozca y mantenga el estado dentro del entorno OpenShift
* Tres maestros para alta disponibilidad
* Las partes en azul son Kubernetes
* Las partes en verde son OpenShift
  * Algunos servicios de infraestructura son exclusivos de OpenShift
  
![Alt text](Imagenes/Nodo-Master.png?raw=true "Arquitectura de alto nivel de OpenShift")

**Los nodos maestros se instalan solo en Red Hat Enterprise Linux CoreOS. No se pueden implementar en RHEL.**

**Los nodos maestros son el motor de orquestación y programación de OpenShift. Son responsables de conocer y mantener el estado del entorno OpenShift.**

### etcd
* Estado actual y deseado en el almacén de datos que se utiliza etcdcomo almacén de valor-clave distribuido
* etcd también contiene:
  * Reglas RBAC
  * Información del entorno de la aplicación
  * Datos de usuario que no pertenecen a la aplicación

![Alt text](Imagenes/etcd.png?raw=true "Arquitectura de alto nivel de OpenShift")

**etcd es un componente crítico de la arquitectura OpenShift. Es el almacén de datos distribuidos de valor clave para el estado y otra información dentro del entorno OpenShift.**

### Master Services - Core Kubernetes Components
* OpenShift incluye los servicios de Kubernetes
* Byte por byte idéntico a Kubernetes de Cloud Native Computing Foundation
* Proporciona:
  * Servidor de API de Kubernetes
  * Programador
  * Servicios de gestión de clústeres
  
![Alt text](Imagenes/services-kubernates.png?raw=true "Arquitectura de alto nivel de OpenShift")

### Master - Infrastructure Services
* Masters y workers colaboran
* Se incluyen los servicios de OpenShift y Kubernetes
* Ejecutar como vainas; orquestado por el plano de control maestro
* Los servicios incluyen:
  * Monitoring
  * Logging
  * OS tuning
  * Software defined networking (SDN)
  * DNS

![Alt text](Imagenes/services-infra.png?raw=true "Arquitectura de alto nivel de OpenShift")

### Master - API and Authentication
* Los maestros proporcionan un único punto final de API con el que interactúan todas las herramientas y sistemas
  * Incluye OpenShift y Kubernetes
  * Todas las solicitudes de administración pasan por esta API
* |Todas las solicitudes de API están encriptadas y autenticadas con SSL
* Autorizaciones manejadas a través del control de acceso basado en roles (RBAC)
* Maestros capaces de vincularse a sistemas de gestión de identidad externos
  * Ejemplos: LDAP, Active Directory, proveedores de OAuth como GitHub y Google
