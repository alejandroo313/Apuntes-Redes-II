# Módulo 3: Nivel de aplicación. Tema 4: Internet of Things
## Introducción
Internet of Things es un paradigma emergente que soporta la integración, transferencia y análisis de los datos generados por dispositivos inteligentes.

IoT significa que cualquier cosa puede comunicarse con cualquier cosa en cualquier lugar, en cualquier momento y utilizando cualquier protocolo. Esto se resume en las 5 A's: Anything, Anywhere, Anytime, Anyway, Anyhow.

## Ecosistema IoT
El ecosistema IoT se basa en tres elementos: dispositivos y controladores o gateways.

![Ecosistema-iot](Ecosistema-iot.png)

<small>DAC: Digital to Analog Converter<small>
<small>ADC: Analog to Digital Converter<small>

### Sensores
Dispositivos que monitorizan y capturan información sobre el entorno. Suelen ser de solo lectura. Se pueden considerar 4 tipos principales:

- Ambientales: luz, presión, temperatura, humedad, etc.
- Biométricos: huella dactilar, glucosa, presión arterial, ritmo cardiaco, etc.
- Proximidad: ultrasonidos, infrarrojos, etc.
- Mecánicos: giroscopios, GPS, inerciales, etc.

![Tipos-sensores](16064064-types-of-sensors.webp)

### Controladores
Elemento central que gestiona y administra la red. Recibe las señales de los sensores, las procesa y toma decisiones sobre ellas (habitualmente basadas en reglas IF-THEN simples), enviando órdenes a los actuadores.

Sus características varían mucho en función de la aplicación, como redes de consumo (smart hoombes, redes personales), o redes comerciales o industriales. Esto influye en:

- Comportamiento: unos están más enfocados que otros en la recolección, agregación y transmisión de datos.
- Periodicidad: en función del uso, necesitarán enviar los datos en tiempo real (cámara Web), o en batch (estación meteorológica).
- Procesamiento: algunos controladores pueden pre-procesar los datos in-situ antes de ser enviados al backend (su volumen es demasiado grande, por ejemplo, o para reducir las comunicaciones).
- Localización: el controlador debe estar en rango de comunicaciones para cualquier sensor o actuador, por lo que el entorno determina mucho su posible localización.
- Seguridad: entornos industriales y de infraestructuras críticas pueden necesitar requisitos de seguridad mayores (como sensores o controladores con medidas físicas anti-manipulación).

### Actuadores
Dispositivos hardware que convierten los comandos del controlador en un cambio físico en el entorno. Estos cambios suelen ser mecánicos (posición, velocidad, …).

Existen diferentes tipos de actuadores:

- Eléctricos: motor, relé, solenoide, servomotor.
- Hidráulicos: cilindros.
- Otros: neumáticos, mecánicos, térmicos, etc.

### Enlaces de comunicación
La función principal de los enlaces de comunicación es servir como conducto o canal que permite la integración, transferencia y comunicación de datos y comandos entre los distintos elementos del ecosistema. Son la columna vertebral y el canal principal entre la capa de aplicación y las actividades operativas del sistema IoT. 

Hay gran diversidad y heterogeneidad de los enlaces de comunicación en IoT. Se clasifican principalmente por el medio físico y la distancia:

- Medio físico:
    - Cableada: tecnologías como Ethernet (cobre, fibra óptica). Ethernet es ideal para grandes cantidades de datos y alta velocidad, pero es vulnerable al daño físico. También se menciona USB.
    - Inalámbrica: más común en IoT. Incluye una amplia gama de tecnologías como Wi-Fi (IEEE 802.11), Bluetooth (incluido BLE), IEEE 802.15.4 (base de ZigBee), 4G/5G, NFC (Near Field Communication), RFID y Satélites.
- Distancia:
    - Corto alcance (PAN - Personal Area Network): Tecnologías como Wi-Fi y RFID se utilizan para gestionar el flujo de datos entre nodos locales.
    - Medio alcance (LAN - Local Area Network): Ethernet puede gestionar conexiones entre múltiples gateways a través de sistemas cableados.
    - Largo alcance (WAN - Wide Area Network): El soporte de redes satelitales y protocolos como 5G ofrecen rangos de comunicación muy largos.

## Protocolos de comunicación
IoT es realmente un agregado de diferentes protocolos y medios de comunicación, como, 4G/5G, WiFi, BT, Ethernet, etc. 

Como suele ocurrir, se están imponiendo protocolos estándar (TCP/IP, ZigBee, o HTTP) frente a propietarios impuestos por los fabricantes.

![Protocolos-comunicacion](image.png)

### CoAP
CoAP (Constrained Application Protocol, RFC7252) es un protocolo de la capa de aplicación y está basado en un conjunto de funcionalidades de HTTP rediseñado para dispositivos de bajo consumo:

- Esta especializado para aplicaciones con interfaz M2M (machine to machine).
- Es un protocolo RESTful, lo que significa que permite la manipulación de recursos. Al igual que HTTP, utiliza métodos como GET, PUT, POST y DELETE.
- Está basado en el protocolo de transporte UDP. Esto permite evitar el overhead y el control de flujo TCP.
- Aunque usa UDP, que inherentemente no es fiable, CoAP proporciona fiabilidad a través de sus mensajes Confirmable (CON).
- Puede operar en modo síncrono y asíncrono.
- Soporta multicast y gestión de congestión.
- La seguridad se implementa sobre DTLS (Datagram Transport Layer Security).

#### Mensajes
CoAP proporciona 4 tipos de mensajes:

- Confirmable (CON): Estos mensajes requieren ser confirmados por el remitente. Si no se recibe respuesta (ACK), se supone que ha habido una perdida y se retransmite.
- No-confirmable (NON): No requieren de confirmación. No ofrecen fiabilidad.
- Confirmación (ACK): Confirmación de mensajes CON.
- Reset (RST): Indica que un mensaje CON o NON fue recibido, pero no procesado correctamente. Puede indicar que el mensaje no es sintácticamente válido o que el receptor no está correctamente configurado.

![Mensajes-coap](image-1.png)

#### Ventajas

- Disminución del retardo (delay).
- Minimización de consumo de recursos debido al uso de UDP y su naturaleza asíncrona.
- Es menos complejo que otros protocolos.
- Ofrece la posibilidad de evitar intermediarios en algunos casos.
- Permite la interoperabilidad con otros estándares.

#### Inconvenientes

- La fiabilidad y la gestión de la congestión (especialmente en el caso de los mensajes NON) pueden ser un inconveniente.
- Madurez.

![COAP](New%20Project.png)

### MQTT
MQTT (Message Queue Telemetry Transport) es otro protocolo de la capa de aplicación del stack de protocolos IoT. Está basado en el esquema publicador/suscriptor simplificado y reducido para IoT:

- Es ligero y potente, capaz de manejar mensajes de hasta 250 MB.
- El uso de TCP le confiere fiabilidad y capacidades de gestión de congestión de tráfico.
- Cuenta con tres roles principales: Publisher (Publicador) que envía mensajes con un topic, Suscriber (Suscriptor) que se suscribe a un tópic y recibe mensajes, y el Broker que orquesta la comunicación entre publicadores y suscriptores. El broker es responsable de informar a los suscriptores cuando los publicadores publican temas de interés y de la seguridad y autenticación.
- Es un protocolo desacoplado en el espacio y tiempo; el publicador no necesita conocer la IP o puerto del destinatario y los mensajes suelen ser asíncronos.

#### Mensajes
MQTT proporciona 15 tipos de mensajes, cada mensaje cuenta con características como Topic, QoS y retención:

- Conexion: CONNECT, DISCONNECT, CONNACK, PINGREQ, PINGRESP, AUTH.
- Publicacion: PUBLISH, PUBACK, PUBRES, PUBREL, PUBCOMP.
- Suscripcion: SUSCRIBE, UNSUSCRIBE, SUBACK, UNPUBACK.

Además, PUBLISH necesita de mensajes dependiendo del QoS del mensaje:

- QoS nivel 0 (At most, one delivery): El mensaje se envía una única vez, sin confirmación (solo PUBLISH).
- QoS nivel 1 (At least one delivery): El mensaje se recibe al menos una vez, (pudiendo) haber retransmisiones (PUBLISH > PUBACK).
- QoS nivel 2 (Exactly one delivery): El mensaje se recibe exactamente una vez (PUBLISH > PUBREC > PUBREL > PUBCOMP).

#### Ventajas

- Fiabilidad (debido a TCP).
- Flexibilidad de QoS.
- Gestión de congestión de tráfico (TCP).
- Mensajes selectivos (topic).
- Cliente ligero.

#### Desventajas

- Necesidad de un bróker central para la comunicación.
- Orientado a conexión (MQTT-SN)

![MQTT](mqtt-publish-subscribe.png)

### Comparación entre CoAP y MQTT

|            | CoAP                                                                 | MQTT                                                                 |
|--------------------------|----------------------------------------------------------------------|----------------------------------------------------------------------|
| **Organismo de estandarización** | IETF                                                                 | OASIS                                                               |
| **Arquitectura**         | Request–Response, Resource “observer”                                | Publish–Subscribe                                                   |
| **Transporte**           | UDP                                                                  | TCP (UDP puede usarse en MQTT-SN)                                   |
| **Seguridad**            | DTLS (transporte), OSCORE (Object Security for Constrained RESTful Environments - aplicación) | TLS (transporte), autenticación de cliente                          |
| **Encabezado**           | 4B + variable                                                        | 2B + variable                                                        |
| **Métodos RESTful**      | GET, POST, PUT, DELETE                                               | No compatible                                                       |
| **Tipos de mensaje**     | 4: CON, NON, RST, ACK                                                | 15: CONNECT, CONNACK, PUBLISH, PUBACK, PUBREC, PUBREL, PUBCOMP, SUBSCRIBE, SUBACK, UNSUBSCRIBE, UNSUBACK, PINGREQ, PINGRESP, DISCONNECT, AUTH |
| **Identificador de recurso** | URI                                                                  | Temas (Topics)                                                      |
| **Fortalezas**           | Ligero, principio de extremo a extremo, asincrónico y sincrónico, flexibilidad y fiabilidad (a través de mensajes CON), interoperabilidad | Asincronía, fiabilidad, simplicidad para el cliente, mensajería selectiva |
| **Limitaciones**         | Transporte no confiable                                              | Dependiente del intermediario (bróker), solo orientado a conexión  |

### ZigBee
ZigBee es una tecnología de comunicación inalámbrica de corto alcance, baja complejidad, bajo consumo de energía, baja velocidad de transmisión de datos y bajo coste. Se sitúa específicamente en la capa de comunicación o la capa de red y enlace dentro del stack de protocolos de IoT.

- Está basada en el estándar IEEE 802.15.4 para su capa física y protocolo de capa de enlace.
- La velocidad de transmisión de datos es baja, alcanzando los 250 Kbit/s. Las velocidades varían según la banda de frecuencia:
    - 868.3 MHz (Europa): un canal, 20 Kbps.
    - 902-928 MHz (América): 10 canales, 40 Kbps.
    - 2.4 GHz (Global): 16 canales, 250 kbps.

En las redes ZigBee, encontramos tres tipos distintos de roles que pueden ser adoptados por los dispositivos:

- Coordinador ZigBee (ZC): Es el dispositivo más completo, actúa como la raíz de la red, almacena información sobre ella, y funciona como centro de confianza y repositorio de claves de seguridad. Solo hay uno por red.
- Router ZigBee (ZR): Actúa como enrutador intermedio, enviando datos entre dispositivos.
- Dispositivo Final ZigBee (ZED): Estos dispositivos solo tienen la funcionalidad de intercambiar datos con su nodo padre (ZC o ZR). No pueden retransmitir datos de otros dispositivos. Esta característica les permite estar en estado de dormido gran parte del tiempo, lo que garantiza una larga duración de la batería y requiere una menor cantidad de memoria y capacidad.

![Red-Zigbee](Imagen-3-600x413.jpg)

### RFID
RFID (Radio-frequency identification) utiliza directamente el campo electromagnético generado por el lector para alimentar una pequeña etiqueta (tag). Esta tecnología se sitúa en la capa física o mencionándose como uno de los medios de comunicación inalámbrica en el stack de protocolos IoT.
Su función principal es la identificación única de objetos. Un sistema RFID consiste de tres grandes elementos:

- Etiqueta RFID: un pequeño chip conectado a una antena, normalmente en forma de espiral.
- Lector: dispone de una antena, que radia la energía necesaria para alimentar la etiqueta y que esta devuelva su identificador. 
- El lector suele disponer, a su vez, de una conexión inalámbrica con su servidor, que contiene los datos asociados a los identificadores.

Comunicación: No requiere comunicación cercana entre la etiqueta y el lector, permitiendo la identificación a distancia sin intervención humana. Existen dos configuraciones comunes:
- "Near" (cercana): El lector tiene una bobina que genera un campo magnético al pasar corriente alterna. La etiqueta, con una bobina más pequeña, genera potencial debido a los cambios en el campo magnético, acoplada a un condensador para alimentar el chip de la etiqueta.
- "Far" (lejana): El lector y la etiqueta tienen antenas dipolo en las que se propagan las ondas electromagnéticas.

![RFID](Basic-RFID-Systen.webp)

### NFC
NFC (Near Field Communication) es una tecnología de comunicación 'contactless' para la comunicación a corta distancia. Esta tecnología se sitúa en la capa física / enlace o capa de red y enlace (Personal Area Network) dentro del stack de protocolos IoT. NFC tiene tres métodos de funcionamiento:

- Peer-to-peer: Permite que dos dispositivos NFC se comuniquen directamente entre si.
- Lector/escritor: Permite acceder a etiquetas NFC.
    - Las etiquetas NFC son un subconjunto de etiquetas RFID que contienen una estructura de memoria sencilla para almacenar datos en un formato estandarizado.
    - El principio básico es "todo esta en un toque", es decir, tocar un objeto con un dispositivo NFC desencadena una acción en ese dispositivo (SMS, llamada, navegación, etc.).
- Emulación de tarjetas: Emula una tarjeta contactless.
    - Los lectores RFID existentes pueden acceder a ella como si fuera una tarjeta corriente.

## Edge-Fog computing
La computación Edge y la computación Fog son uno de los paradigmas de computación distribuida emergentes, propuestos para superar las limitaciones del paradigma de cloud computing centralizado en el contexto del creciente ecosistema IoT. 

La idea principal es acercar el procesamiento a los dispositivos IoT:

- Disminuir el tiempo de acceso y latencia desde los dispositivos IoT a los servidores.
- Mientras se maximiza la capacidad de cómputo, fiabilidad y almacenamiento.
- Soportado por los proveedores de servicio principales: AWS IoT, Azure IoT edge, Watson IoT.

![Google-edge-computing](image-2.png)

### Ejemplos
Wearables: en lugar de transmitir todos los datos a servidores "centrales", se pre-procesan en los móviles de los usuarios. Solo se envían datos agregados y procesados en tandas.

Granjas inteligentes: Se coloca un hub (servidor) en la granja, que realiza el pre-procesamiento de datos. En función de la aplicación, este hub puede tener más o menos funcionalidades.

![Piramide-ejemplo](image-3.png)

### Diferencias entre Cloud y Fog/Edge computing

|  | Cloud | Fog/Edge |
|----------------|--------|----------|
| **Localización** | Centralizados en un pequeño número de centros de datos. | Distribuidos en distintas localizaciones, geográficamente situadas, con el objetivo de estar cerca de los usuarios. |
| **Tamaño** | Los centros de datos que dan soporte a los sistemas cloud, normalmente están compuestos por miles de nodos computacionales. | Variable. Puede ser de tamaño pequeño (por ejemplo, un único nodo en una planta de fabricación o a bordo de un vehículo) o tan grande como sea necesario para satisfacer las demandas de los clientes. |
| **Apps.** | Las aplicaciones deben poder soportar tener una latencia media-alta. | Permiten aplicaciones en tiempo real, que necesitan tiempos de latencia críticamente bajos para su correcto funcionamiento (<10ms). |

### Diferencias entre Fog y Edge computing

|             | Fog Computing                                                                                  | Edge Computing                                                                                   |
|--------------------------|------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Definición**           | Arquitectura distribuida que extiende la nube hacia el borde de la red.                        | Paradigma que lleva la computación directamente a los dispositivos en el borde de la red.       |
| **Ubicación del procesamiento** | Entre la nube y los dispositivos finales (enrutadores, gateways, servidores locales).          | Directamente en los dispositivos finales (sensores, smartphones, actuadores, etc.).             |
| **Proximidad al usuario**| Cercano al usuario, pero no necesariamente en el dispositivo final.                            | Muy cercano o en el propio dispositivo del usuario.                                              |
| **Enfoque**              | Infraestructura intermedia para filtrar, procesar y enviar datos relevantes a la nube.         | Procesamiento local inmediato para minimizar latencia y dependencia de la nube.                 |
| **Ejemplos de dispositivos** | Gateways, switches inteligentes, micro data centers, routers.                                | Smartphones, smartwatches, sensores inteligentes, dispositivos IoT.                             |
| **Latencia**             | Baja, pero puede involucrar múltiples saltos desde el dispositivo hasta el nodo fog.            | Muy baja (tiempo real), ya que el procesamiento ocurre en el mismo dispositivo o en uno cercano.|
| **Escalabilidad**        | Alta, permite distribuir tareas entre múltiples nodos intermedios.                             | Limitada por los recursos del dispositivo de borde.                                              |
| **Mantenimiento**        | Requiere gestión de múltiples nodos y sincronización con la nube.                             | Menor mantenimiento; generalmente autónomo y distribuido.                                       |
| **Privacidad y seguridad** | Alta, ya que los datos pueden procesarse localmente sin enviarse a la nube.                   | Muy alta, el usuario puede tener control total sobre los datos en su propio dispositivo.         |
| **Casos de uso típicos** | Sistemas de tráfico inteligente, ciudades inteligentes, fábricas con IoT distribuido.          | Smart homes, sensores de salud portátiles, procesamiento local en dispositivos móviles.          |
| **Relación con la nube** | Actúa como un intermediario entre la nube y el borde.                                          | Puede operar independientemente de la nube.                                                      |

## Ventajas
Las ventajas de IoT abarcan todos los ámbitos del estilo de vida y de los negocios. Entre ellas podemos encontrar:

- Seguimiento y monitorización de datos de usuarios, animales u objetos. Localización del usuario mediante GPS, contabilización de la distancia recorrida, ritmo cardiaco. Por ejemplo los relojes inteligentes para deportistas.
- Reducción de esfuerzo: Los dispositivos IoT se comunican e interactúan entre sí, proporcionan automatización de las tareas.
    - Reducir la necesidad de intervención humana.
- Reducción de gasto: A través de la monitorización del uso de los recursos, puede ajustarse la cantidad de elementos necesarios de un sistema.

## Inconvenientes
IoT también presenta un importante conjunto de retos:

- Seguridad: IoT crea un ecosistema de dispositivos conectados constantemente. Pese a que se implementan distintas directivas de seguridad, se encuentran más expuestos a ataques.
- Privacidad: Proporciona datos personales altamente sensibles sin la participación activa del usuario.
- Complejidad: Algunos diseños de sistemas pueden ser altamente complejos en términos de diseño, despliegue y mantenimiento, debido a las distintas tecnologías y protocolos utilizados. 
- Estandarización: Pese a los avances realizados en los últimos años. Hay dificultades asociadas a las estandarizaciones y su cumplimiento por parte de los fabricantes.