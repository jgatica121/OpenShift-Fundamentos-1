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
