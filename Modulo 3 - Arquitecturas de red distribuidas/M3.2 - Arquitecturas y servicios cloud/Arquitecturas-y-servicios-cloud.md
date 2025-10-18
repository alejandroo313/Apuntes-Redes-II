# Módulo 3: Nivel de aplicación. Tema 2: Arquitecturas y Servicios Cloud
## ¿Qué es cloud computing?
El cloud computing, o computación en la nube, se describe como un modelo para habilitar el acceso bajo demanda a través de la red a un conjunto de recursos de computación configurables (redes, servidores, almacenamiento, aplicaciones y servicios). Estos recursos pueden ser rápidamente aprovisionados y liberados con un esfuerzo mínimo de gestión o interacción con el proveedor de servicios.  
De manera más concisa, es una forma especializada de computación distribuida que introduce el uso de modelos para aprovisionar de manera remota recursos escalables y medidos.
### Características claves de los sistemas cloud
Las características clave que deben cumplir los sistemas cloud, según los estándares de la industria como NIST (National Institute of Standards and Technology) son:

- Bajo demanda: El usuario puede solicitar unilateralmente el servicio (post-pago)
- Acceso universal/ubicuidad: El sistema debe ser accesible a través de distintos tipos de dispositivos distribuidos geográficamente.
- Acceso compartido/multilatencia: Los recursos se comparten entre múltiples usuarios que acceden de manera concurrente, lo que se facilita mediante la virtualización.
- Escalabilidad y elasticidad: El sistema debe ser capaz de escalar sus recursos de mantera transparente al usuario. Esta adaptación a la demanda es considerada la clave angular de los sistemas cloud y permite la reducción de costes. Esto incluye tanto el escalado horizontal (incremento/decremento de recursos del mismo tipo) como el vertical (cambio de recursos de mayor/menor capacidad).
- Medición: Proporciona una visión detallada del uso de la plataforma, lo que permite el modelo de pago por uso donde solo se factura el uso real de los recursos.
- Resiliencia: Capacidad del sistema para recuperarse de fallos, a menudo mediante redundancia.

### Tipos de servicios cloud
Los sistemas cloud ofrecen distintos tipos de servicios (modelos de entrega), que se diferencian por el nivel de abstracción y gestión que el proveedor ofrece y el usuario asume:

- Infraestructura como servicio (IaaS): El proveedor proporciona la infraestructura fundamental, como máquinas virtuales, almacenamiento y redes. El usuario instala y gestiona sus propios sistemas operativos y software. Un ejemplo es AWS (Amazon Web Services).
- Plataforma como servicio (PaaS): Además de la infraestructura, el proveedor incluye hardware, sistemas operativos y herramientas de desarrollo y administrativas. El usuario se enfoca en desarrollar y desplegar su software. Heroku es un ejemplo de este tipo de plataformas.
- Software como servicio (SaaS): El proveedor ofrece una aplicación completa lista para usar, accesible a través de una interfaz de usuario. Ejemplos comunes son Google Docs y Gmail.
- Existen otras categorías de servicios como Funciones, almacenamiento, bases de datos, seguridad, etc., como servicio (FaaS, Storage as a Service, Database as a Service, etc.).

![Tipos-de-servicios](Tipos-de-servicios.png)

### Modelos de despliegue (Tipos de cloud)
Los modelos de despliegue describen donde y como se implementa el cloud:

- Cloud publico: Gestionado por grandes empresas y disponible para cualquier usuario que desee contratarlo. Suele ser el más económico pero percibido como el menos seguro.
- Cloud privado: Propiedad de una entidad especifica y utilizado exclusivamente por ella. Es más costoso pero más seguro.
- Cloud comunitario: Compartido por múltiples organizaciones con intereses comunes.
- Cloud hibrido: Una combinación de dos o más clouds (públicos, privados o comunitarios) que permanecen como entidades únicas, pero se interconectan, permitiendo, por ejemplo, usar un cloud privado para datos sensibles y uno público para datos menos sensibles.
- Cloud privado virtual: Esencialmente un cloud privado dentro de un cloud público.
- Multi-Cloud: Utilización de servicios de múltiples proveedores de cloud, como Amazon, Google y Azure.
- Cloud distribuido: Combina nodos de cómputo ubicados en distintas localizaciones.

![Modelos-de-despliegue](Modelos-de-despliege.png)

## Antecedentes
Hay una serie de conceptos directamente relacionados con cloud computing que son interesantes mencionar:
### Virtualización
La virtualización es un componente básico en las infraestructuras IT. Surgió para mejorar el bajo porcentaje de uso del hardware físico. Permite ejecutar múltiples sistemas virtuales aislados en un único sistema físico, proporcionando entornos de ejecución aislados.
#### Hipervisor
El hipervisor es identificado como un mecanismo fundamental para la virtualización de infraestructuras, siendo el actor principal en la creación de máquinas virtuales (VMs) a partir de un servidor físico. Un hipervisor generalmente se limita a un único servidor físico y gestiona el control, el uso compartido y la planificación de recursos de hardware como procesadores, memoria y almacenamiento.

- Hipervisor tipo 1: También denominado nativo, unhosted o bare metal, es software que se ejecuta directamente sobre el hardware físico, para ofrecer la funcionalidad descrita. Las máquinas virtuales se ejecutan sobre él y todos los accesos directos a hardware son controlados por el hipervisor. (Ejemplo: Oracle VM Server, Microsoft Hyper-V).
- Hipervisor tipo 2: También denominado hosted, sobre el hardware físico se ejecuta un sistema operativo anfitrión el cual ejecuta el hipervisor que es una aplicación de virtualización que se encarga de ofrecer la funcionalidad descrita. (Ejemplos: VMware Workstation, Virtualbox)
- Hypervisor hibrido: Sobre el hardware se ejecuta un sistema operativo anfitrión y el hipervisor. El hipervisor a veces interacciona directamente sobre el hardware, pero otras veces usa servicios que le proporciona el sistema operativo anfitrión.

#### Contenedores
Los contenedores (Dockers) empaquetan aplicaciones, dependencias y librerías del sistema en un contenedor, siendo una imagen Docker un paquete de software ligero, independiente y ejecutable que incluye todo lo necesario para ejecutar una aplicación. Aparte, son disponibles para múltiples sistemas operativos.

![Hipervisores-contenedores](virtualizacion.png)

En el contexto de las Arquitecturas y servicios cloud, la virtualización es crucial porque:

- Habilita características clave del cloud: Es la base para el acceso compartido (mutlilatencia) y la agrupación de recursos ("Resourde Pooling"), permitiendo que múltiples usuarios compartan la infraestructura subyacente de manera eficiente y aislada.
- Es fundamental para los modelos de servicio: Particularmente para Infraestructura como Servicio (IaaS), donde los proveedores ofrecen máquinas virtuales como un servicio gestionable por el usuario.
- Soporta arquitecturas y mecanismos cloud: Mecanismos de infraestructura como el Servidor Virtual y mecanismos especializados como el Hipervisor, ambos directamente basados en la virtualización.
- Es una tecnología habilitadora: Junto con las redes de banda ancha, la arquitectura de Internet, la tecnología de centros de datos, la tecnología web, la multitendencia y la tecnología de servicios, la virtualización (especialmente la moderna) es una de las tecnologías que, aunque existía antes del cloud, fue refinada para permitir las plataformas cloud actuales.

### Recurso IT
Un recurso IT es un artefacto físico o virtual que puede estar basado en software o hardware y forma parte de una infraestructura IT. Ejemplos de recursos IT:

- Recursos Físicos: Servidor físico, almacenamiento, dispositivo de red.
- Recursos Lógicos: Servidor virtual, software, servicio, queue.

### Escalado
El escalado representa la habilidad del Recurso IT a incrementar o decrementar sus capacidades bajo demanda. Esta habilidad es fundamental en el cloud computing. Hay dos tipos principales de escalado:

- Escalado vertical: Implica la sustitución por Recursos IT de mayor o menor capacidad. 
- Escalado horizontal: Implica el incremento o decremento de Recursos IT del mismo tipo.

Reemplazar un Recurso IT por uno de mayor capacidad es "scaling up", y por uno de menor capacidad es "scaling down". El escalado vertical es menos común en entornos cloud debido al tiempo de inactividad que normalmente requiere el reemplazo.  
El escalado es una característica clave de los sistemas cloud y se describe como la clave angular de estos sistemas. La escalabilidad y elasticidad se refieren a la capacidad del sistema para escalar sus recursos de manera transparente al usuario. Esta adaptación a la demanda es crucial para la reducción de costes.

![Comparación-escalado](1709242524105.webp)

### Carga de trabajo
La carga de trabajo, o workload, es una aplicación especifica, servicio, capacidad o cantidad de trabajo a ser ejecutado sobre una infraestructura y que consume sus recursos. Representa la demanda que se impone a la infraestructura IT. Hay diferentes tipos de cargas de trabajo, clasificadas según el patrón de uso de los Recursos IT que generan:

- Estática: Los recursos IT se utilizan de manera equitativa y sin variaciones durante el tiempo de ejecución del workload.
- Periódica: Los recursos IT reciben un uso máximo (peak) en intervalos recurrentes.
- Una-vez-en-la-vida (one-life-a-time): Los Recursos IT reciben un uso inusual y extremadamente alto, un caso que sucede una vez en la vida de la infraestructura.
- Impredecible: Los Recursos IT reciben un uso impredecible y aleatorio.
- En cambio continuo: Los recursos IT experimentan un cambio continuo de uso.

### SLA (Service Level Agent)
Los SLAs son documentos (contratos) legibles por humanos, proporcionado por los proveedores de servicio. Estos contratos se establecen entre un proveedor cloud y un consumidor cloud. La finalidad principal de un SLA es describir características relacionadas con la calidad de servicio (QoS), así como garantías y limitaciones de una o más infraestructuras cloud o servicios cloud. Las condiciones de uso de los servicios cloud suelen expresarse típicamente en un SLA.  
Los SLAs usan métricas de QoS. Estas métricas proporcionan detalles de varias características medibles relacionadas con los resultados de IT. Las métricas incluyen:

- Disponibilidad: tiempo de actividad, interrupciones, duración del servicio.
- Fiabilidad: tiempo mínimo entre fallos, tasa garantizada de respuestas satisfactorias.
- Rendimiento: garantías de capacidad, tiempo de respuesta y tiempo de entrega.
- Escalabilidad: garantías de fluctuación de capacidad y capacidad de respuesta.
- Resiliencia: tiempo medio de conmutación y recuperación. 

Es crucial que estas métricas sean cuantificables, repetibles, comparables y fácilmente obtenibles.

### Clúster
Un clúster es una colección de nodos de computación integrados como un único recurso IT o, de manera similar, como un grupo de recursos IT independientes que están interconectados y funcionan como un único sistema. Estos nodos suelen ser computadoras comerciales con software de licencia abierta.
El objetivo de los clústeres es reducir las tasas de fallo e incrementar la disponibilidad y fiabilidad. Esto se consigue gracias a características inertes de redundancia y conmutación por error (failover).  
Los nodos dentro de un clúster están interconectados a través de una red local de alta velocidad y baja latencia, y su gestión se realiza a través de un nodo front-end. En los clústeres de hardware, es un requisito general que los sistemas componentes tengan hardware y sistemas operativos razonablemente parecidos para asegurar nieves de rendimiento similares si un componente falla. La sincronización entre los dispositivos se mantiene mediante enlaces de comunicación dedicados de alta velocidad.

### Grid
Grid computing es una forma especializada de computación distribuida. En este modelo, múltiples recursos informáticos, también llamados nodos grid, proporcionan en colaboración una gran capacidad de cálculo. Estos recursos pueden incluir clústers, supercomputadoras, datos, sistemas de almacenamiento, servicios, etc.
En los grid, los recursos IT que los componen están más débilmente acoplados. Además, pertenecen a múltiples dominios administrativos geográficamente dispersos y se conectan a través de internet. La orquestación de estos recursos se realiza a través de middleware.

A pesar de tener similitudes con los clusters, existen diferencias clave. En el grid se menciona una computación sin comunicación con otros nodos y una falta de red de alta velocidad entre ellos, características que si son comunes en los clusters. Los sistemas Grid son mucho más débilmente acoplados y distribuidos que los sistemas basados en clusters, lo que permite incluir recursos heterogéneos y gráficamente dispersos, algo que generalmente no es posible con los clsters.

### Profundiza
- ¿Qué ventajas e inconvenientes tienen los dos tipos de escalado?

| Tipo de Escalado     | Ventajas                                                                                          | Inconvenientes                                                                 |
|----------------------|---------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| **Escalado Horizontal** | - Menos costoso (usa hardware comercial)   - Recursos IT disponibles instantáneamente  - Soporta replicación de recursos y escalado automatizado  - No está limitado por la capacidad máxima del hardware | - Requiere configuración adicional  - Requiere recursos IT adicionales     |
| **Escalado Vertical**   | - Recursos IT disponibles instantáneamente  - No se necesitan recursos IT adicionales       | - Más costoso (usa servidores especializados)  - Requiere configuración adicional  - Limitado por la capacidad máxima del hardware |

- Dibuja gráficos que ilustren los 5 tipos de carga de trabajo
- ¿En qué casos es más conveniente utilizar un clúster? ¿Y un Grid?
    - Casos más convenientes para un Clúster: Cuando se necesita alta disponibilidad y fiabilidad para aplicaciones críticas que no pueden tolerar fallos. Cuando se requiere un alto rendimiento y una comunicación rápida y de baja latencia entre los nodos, como en ciertas cargas de trabajo de computación de alto rendimiento (HPC) o bases de datos en clúster. Ideal para recursos informáticos localizados geográficamente de forma cercana que pueden ser gestionados como una unidad unificada.
    - Casos más convenientes para un Grid: Cuando se necesita agregar una gran cantidad de capacidad de cálculo de recursos distribuidos geográficamente y posiblemente heterogéneos. Ideal para cargas de trabajo que se pueden dividir en muchas tareas independientes que no requieren una comunicación intensiva o de baja latencia entre sí (lo que a menudo se denomina problemas "embarrassingly parallel", aunque la fuente no utiliza este término). Útil para compartir recursos computacionales entre diferentes organizaciones o departamentos.

## Diagrama General de un servicio cloud
![Diagrama-general](Captura%20desde%202025-05-02%2018-11-33.png)

## Tipos de servicios cloud: OpenStack
OpenStack es un proyecto de código abierto que proporciona todos los mecanismos para construir sistemas cloud. Se describe como el proyecto open-source más extendido de todo el mundo.  
Dentro del contexto de los tipos de servicios cloud, OpenStack proporciona o permite la gestión de una amplia gama de recursos de TI. Permite la creación y gestión de elementos primarios ("building-blocks") para construir sistemas masivos. A traves de OpenStack, se busca dar sensación de recursos infinitos mediante la gestión masiva de recursos IT.  
Ofrece IaaS, PaaS, SaaS y más y cuenta con 25M de cores en producción.
OpenStack cuenta con una arquitectura modular, construida sobre servicios elementales que están en crecimiento. Los más importantes son: Horizon, Nova, Glance, Swift, Quantum, Cinder y Keystone

![OpenStack](OpenStack_Map.svg.png)

### Dashboard (Horizon)
Horizon: Dashboard de la plataforma, proporciona una interfaz de usuario sencilla para usuarios finales. Horizon es utilizado tanto por los usuarios finales como por los administradores de sistemas cloud. Para los usuarios finales, ofrece una interfaz sencilla. Para los administradores, proporciona funciones básicas de administrador de sistemas cloud, como la definición de usuarios, "tenants" (inquilinos) y cuotas. Además, ofrece una interfaz gráfica para el acceso, la provisión y automatización de los recursos.  
En el contexto de los servicios elementales, Horizon actúa como la capa de interfaz de usuario que permite a los usuarios y administradores gestionar y acceder a los recursos y funcionalidades proporcionadas por los otros servicios modulares de OpenStack.  
Históricamente, Horizon se incluyó como un componente en las versiones de OpenStack a partir de la versión Essex, lanzada el 5 de abril de 2012.

![Dashboard](image.png)

### Identificacion (Keystone)

- Framework de uso común para gestionar autorizaciones. 
- Se encarga de la gestión de usuarios, "tenants" y roles.
- Proporciona un directorio central de usuarios asignados a los servicios de OpenStack que pueden acceder.
- Puede interactuar con distintos backends para la gestión de entidades, como SQL, MAriaDB, LDAP, IDM...
- Soporta múltiples formas de autenticación, incluyendo credenciales estándar (nombre de usuario y contraseña), sistemas basados en tockens e inicios de sesión al estilo AWS.

En el contexto de los servicios elementales de OpenStack, Keystone juega un papel fundamental como el punto central para la autenticación y autorización.  
La inclusión de Keystone como componente de OpenStack data al menos desde la versión Essex, lanzada en abril de 2012, según el historial de versiones, lo que subraya su importancia y su integración temprana en la plataforma modular.

![Identificación](Captura%20desde%202025-05-03%2009-57-52.png)

### Computo (Nova)
OpenStack Compute, conocido como Nova, es identificado como uno de los servicios elementales más importantes y un componente clave de OpenStack. Su rol principal es ser el Servicio de cómputo.

- Es la parte principal de un sistema IaaS.
- Está diseñado para gestionar y automatizar los pools de los recursos del equipo.
- Puede trabajar con tecnologías de virtualización ampliamente disponibles.
- Gestiona las Máquinas Virtuales (VMs) a través de nodos de cómputo, utilizando hipervisores como KVM, Xen, LXC, Hyper-V y ESX. También se menciona la capacidad de trabajar con tecnología de contenedores Linux como LXC.
- Incluye controladores distribuidos que gestionan la planificación y llamadas a las APIs: compatible con Amazon EC2 API.
- Su arquitectura está diseñada para escalar horizontalmente. 

Históricamente, Nova es uno de los componentes más antiguos de OpenStack, habiendo sido incluido en la primera versión, Austin, lanzada el 21 de octubre de 2010. Esto refuerza su estatus como servicio elemental y fundacional de la plataforma.

![Computo](Captura%20desde%202025-05-03%2010-10-33.png)

### Gestión de imágenes (Glance)
Glance es un servicio de gestión de imágenes. Almacena y gestiona imágenes de disco (plantillas de VM).

- Proporciona servicios de descubrimiento, inscripción y entrega de discos y del servidor de imágenes.
- Puede utilizarse para almacenar y catalogar un número ilimitado de copias de seguridad.
- Soporta varios formatos de imagen, incluyendo Raw, QCOW, VMDK, VHD, ISO y AMI/AKI.
- Glance puede almacenar imágenes en la una variedad de back-ends, como Filesystem, Swift y Amazon S3. La capacidad de usar OpenStack Object Storage (Swift) como back-end ilustra la interconexión y dependencia entre los distintos servicios elementales.
- La API del servicio de imagen proporciona una interfaz REST estándar para consultar información sobre las imágenes de disco y permite a los clientes transmitir las imágenes a nuevos servidores.

Históricamente, Glance se incluyó como un componente en las versiones de OpenStack a partir de la versión Bexar, lanzada el 3 de febrero de 2011, lo que indica que fue reconocido tempranamente como un módulo central y necesario para la operación básica de una nube OpenStack IaaS (Infraestructura como Servicio).
![Gestión-de-imágenes](Captura%20desde%202025-05-03%2010-04-04.png)

### Almacenamiento de objetos (Swift)
OpenStack Object Storage, conocido como Swift, es identificado explícitamente como uno de los servicios elementales más importantes y un componente de OpenStack. Su función principal es ser el servicio de almacenamiento de objetos.

- Es un sistema de almacenamiento redundante y escalable. 
- Los objetos y archivos se escriben en varias unidades de disco repartidas por los servidores del centro de datos.
- El software de OpenStack (Swift) es responsable de asegurar la replicación y la integridad de los datos en el clúster.
- Fue modelado después del servicio S3 de Amazon.
- Proporciona una API nativa y una API compatible con S3.
- Permite almacenar diversos tipos de datos (objetos, VMs, isos, etc.).
- Glance, el servicio de imagen, puede utilizar OpenStack Object Storage (Swift) como uno de sus back-end para almacenar imágenes de disco y servidor.

Históricamente, Swift es uno de los componentes fundacionales de OpenStack, habiendo sido incluido en la primera versión, Austin, lanzada el 21 de octubre de 2010. Fue desarrollado originalmente por Rackspace.
![Almacenamiento-de-objetos](Captura%20desde%202025-05-03%2010-15-16.png)

### Red de comunicaciones (Neutron)
OpenStack Networking, conocido como Neutron, es identificado explícitamente como uno de los servicios elementales más importantes y un componente clave de OpenStack. Su función principal, según las fuentes, es ser el Servicio de red de comunicaciones o Networking.

- Es un sistema para la gestión de redes y direcciones IP.
- Asegura que la red no sea un cuello de botella o factor limitante en un despliegue en la nube.
- Ofrece a los usuarios un autoservicio real para sus configuraciones de red.
- Proporciona modelos de redes para diferentes aplicaciones o grupos de usuarios. Los modelos estándar incluyen redes planas o VLAN para separar servidores y tráfico.
- Gestiona las direcciones IP, incluyendo estáticas, DHCP reservadas y direcciones IP flotantes, que permiten redirigir el tráfico dinámicamente a cualquier recurso informático (útil durante mantenimiento o fallos).
- Los administradores pueden aprovechar tecnologías de redes definidas por software (SDN) como OpenFlow para lograr altos niveles de multi-inquilino (multitenancy) y escala masiva.
- Tiene una arquitectura basada en plug-ins.
- Permite integrar soluciones de red basadas en hardware y software.
- Su framework permite la extensión de servicios de red adicionales como sistemas de detección de intrusos (IDS), balanceo de carga, cortafuegos y redes privadas virtuales (VPN).

Históricamente, el servicio de red de OpenStack fue conocido inicialmente como Quantum. Las fuentes indican que Quantum fue incluido como componente a partir de la versión Folsom (lanzada el 27 de septiembre de 2012). Posteriormente, el nombre del componente cambió a Neutron a partir de la versión Havana (lanzada el 17 de octubre de 2013). Esto muestra la evolución de la plataforma y cómo los nombres de los servicios elementales pueden cambiar.
![Red-de-comunicaciones](Captura%20desde%202025-05-03%2010-19-26.png)

### Gestión de volúmenes (Cinder)
OpenStack Block Storage, conocido como Cinder, es identificado explícitamente como uno de los servicios elementales más importantes y un componente de OpenStack. Su función principal, según las fuentes, es ser el Servicio de gestión de volúmenes o Block Storage.

- Proporciona dispositivos de almacenamiento a nivel de bloque persistentes para usar con instancias de OpenStack Compute (Nova).
- Gestiona la creación, aplicación (attachment) y el desprendimiento (detachment) de los dispositivos de bloque a los servidores.
- Los volúmenes de almacenamiento en bloque se integran completamente con OpenStack Compute y el Dashboard (Horizon), lo que permite a los usuarios de la nube gestionar sus propias necesidades de almacenamiento.
- Ofrece gestión de snapshots para realizar copias de seguridad de los datos guardados en volúmenes y utilizarlas para restaurar o crear nuevos volúmenes.
- Las fuentes comparan Cinder con el servicio Amazon EBS.

En el contexto más amplio de los servicios elementales (módulos), Cinder es un componente fundamental porque gestiona un tipo crucial de recurso IT: el almacenamiento persistente a nivel de bloque. Mientras que Swift gestiona el almacenamiento de objetos (datos no estructurados a gran escala), y Glance gestiona las imágenes de disco (plantillas para VMs), Cinder proporciona los "discos duros" virtuales que se pueden adjuntar a las máquinas virtuales (instancias de Nova) para almacenamiento duradero, incluso si la instancia de cómputo se elimina o se reinicia. Su funcionalidad es esencial para muchas aplicaciones empresariales y cargas de trabajo que requieren sistemas de archivos tradicionales o bases de datos instaladas directamente en las VMs.

Históricamente, las fuentes indican que Cinder fue incluido como componente de OpenStack a partir de la versión Folsom, lanzada el 27 de septiembre de 2012. Esto, junto con otros servicios como Quantum (luego Neutron), Glance y Keystone, se añadió a los componentes iniciales de Nova y Swift, evidenciando el crecimiento de la plataforma OpenStack a través de la adición de nuevos servicios elementales.
![Gestión-de-volúmenes](Captura%20desde%202025-05-03%2010-23-15.png)

### Esquema general
![Esquema-general](IMG_1903.JPG)

## Factores económicos de los sistemas cloud
El coste total de propiedad, o total cost of ownership (TCO), es presentado como uno de los factores más importantes a considerar al abordar la adopción de un sistema cloud. Tradicionalmente, el TCO de un servidor físico incluye costes directos (precio inicial, energía, espacio, almacenamiento, operaciones IT), costes indirectos (infraestructura de red y almacenamiento, gestión de infraestructura general), y costes generales (personal de administración).    
Los sistemas cloud, construidos sobre arquitecturas de servicios elementales y modulares como OpenStack, introducen un modelo económico fundamentalmente diferente. La principal ventaja económica destacada es la reducción o eliminación de las inversiones iniciales en IT. Los proveedores cloud, al adquirir recursos IT de forma masiva, pueden ofrecer paquetes de alquiler a precios atractivos, reemplazando los gastos de capital (CapEx) por gastos operacionales medidos (OpEx). Esto se conoce como costes proporcionales.  
Se presentan las 10 leyes de Cloudonomics, un conjunto de principios que explican las ventajas económicas derivadas de la arquitectura y el modelo operativo del cloud:

1. Los servicios cuestan menos, aunque cuestan más: los clientes no pagan cuando no usan los servicios.
2. La demanda triunfa sobre la previsión: el cloud permite gestionar la demanda sin incurrir en costes por previsiones erróneas.
3. El pico de la suma nunca es mayor que la suma de los picos: la demanda agregada de múltiples clientes suaviza las variaciones, mejorando la eficiencia.
4. La demanda agregada... tiende a suavizar las variaciones. (Refuerza el punto anterior).
5. Los costes medios unitarios se reducen distribuyendo los costes fijos. (Principio de economías de escala).
6. La superioridad numérica es el factor más importante: los CSPs tienen la escala para luchar contra ataques, lo que implica un ahorro en seguridad.
7. El espacio-tiempo es continuo: se aumenta el valor reduciendo el tiempo de operaciones y toma de decisiones. (Valor económico derivado de la agilidad).
8. La dispersión es el cuadrado inverso de la latencia: permite reducir la latencia con más nodos de los que se tendrían convencionalmente. (Valor económico derivado de la mejora del rendimiento y alcance).
9. No ponga todos los huevos en la misma cesta: alta fiabilidad con muchos centros de datos por CSP. (Valor económico derivado de la resiliencia y reducción de riesgos de fallo).
10. Un objeto en reposo tiende a permanecer en reposo: los centros de datos en la nube están situados en ubicaciones óptimas frente a los privados. (Valor económico derivado de la optimización geográfica).

## Ventajas
### Coste de los procesos
Bajos costes iniciales, ya que no hay barreras de adopción. Se eliminan los costes fijos, y los costes variables van en función de la facturación.

### Mayor calidad y agilidad en los procesos
La escalabilidad dinámica permite a los sistemas cloud adaptar recursos a la demanda de manera transparente. Esto evita los costes o pérdidas de negocio asociadas a una previsión errónea (sub-aprovisionamiento o sobre-aprovisionamiento). La provisión bajo demanda contribuye a esta agilidad.

### Modelo as-a-service
El modelo de uso "as-a-service", donde los detalles técnicos y operativos se abstraen del consumidor, ofrece ahorros al empaquetar la funcionalidad en soluciones "listas para usar". Esto simplifica y agiliza el desarrollo, despliegue y administración de recursos IT, generando "ahorros significativos de tiempo y de necesidad de experiencia IT especializada".

### Nuevos modos de provisión de servicios y modelos de negocio
El cloud permite la provisión de servicios propios usando este nuevo modelo. También facilita la integración con proveedores cloud y el aprovechamiento del ecosistema, generando nuevas ventajas competitivas y modelos de negocio.

## Inconvenientes
### Seguridad
Preocupación fundamental. ¿Están nuestros datos seguros?, ¿Cómo se puede auditar la seguridad?, ¿Serán mis datos eliminados en caso de borrar mi cuenta?

### Conformidad
Se plantea la duda de si se cumplirán las leyes y regulaciones sobre riesgos, seguridad y privacidad. Esto se corresponde con los problemas de "Multi-Regional Compliance and Legal Issues" (Cumplimiento multirregional y cuestiones legales), especialmente porque la ubicación geográfica de los datos y recursos IT puede estar fuera del control del consumidor cuando están alojados por un proveedor tercero.

### Interoperabilidad (vendor lock-in)
Un inconveniente clave es la dificultad o la imposibilidad de trasladar la carga de trabajo (workload) de un proveedor cloud a otro. Esto se debe a la "Limited Portability Between Cloud Providers" (Portabilidad limitada entre proveedores cloud). La portabilidad puede verse limitada por dependencias de características propietarias impuestas por un cloud y por la falta de estándares establecidos en la industria cloud.

### Service Level Management
¿Es correcta la facturación?, ¿Que ocurre en caso de fallo?, ¿Es suficiente la capacidad?
Este conjunto de puntos se relaciona con el "Reduced Operational Governance Control" que los consumidores cloud suelen tener, el cual es menor que el que tendrían sobre recursos IT on-premise. Esto introduce riesgos asociados a cómo el proveedor cloud opera su infraestructura. Ejemplos de esto incluyen proveedores poco fiables que no cumplen las garantías de los SLAs (Service Level Agreements) o problemas de latencia y ancho de banda debido a la distancia geográfica.