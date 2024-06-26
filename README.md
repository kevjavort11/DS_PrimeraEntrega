# **Data Science I : Fundamentos para la Ciencia de Datos**

**1RA PRE ENTREGA**

**Fecha: 25/06/2024**

**Estudiante : Ortega Hernandez Kevin Javier**

**Objetivos**


1. *Preparación de hipótesis* 
2. *Visualizaciones multivariables*
3. *Relación de gráficos - hipotesis*
4. *Identificación de datos nulos*
5. *Hallazgos de las variables relevantes*


# **Dataset:**

[CTU-IoT-Malware-Capture-48-1](https://docs.google.com/spreadsheets/d/16rvHjh1RfR3YSPoao5vYDXLG3CG1SZYcNRssSlaEe3U)

# **Abstract:**

El dataset *CTU-IoT-Malware-Capture-48-1* consta de veintitrés capturas de diferentes tráficos de red IoT. Estos escenarios se dividen en veinte capturas de red de dispositivos IoT infectados (que tendrán el nombre de la muestra de malware ejecutada en cada escenario) y tres capturas de red de tráfico real de dispositivos IoT. 

En cada escenario malicioso se ejecuto una muestra de malware específica en una Raspberry Pi, que utilizó varios protocolos y realizó diferentes acciones. 

El tráfico de red capturado para los escenarios benignos se obtuvo capturando el tráfico de red de tres dispositivos IoT diferentes: una lámpara LED inteligente Philips HUE, un asistente personal inteligente para el hogar Amazon Echo y una cerradura inteligente Somfy. 

Tanto los escenarios maliciosos como los benignos se ejecutan en un entorno de red controlado con conexión a internet sin restricciones como cualquier otro dispositivo IoT real.







# **Diccionario de Datos**

1. **Unnamed: 0**: Indice de columna.
2. **duration**: Duracion de la conexion en segundos (s).
3. **orig_bytes**: Numeros de bytes enviados por el originator.
4. **resp_bytes**: Numero de bytes enviados por el responder.
5. **local_orig**: Indica si el originator es local.
6. **local_resp**: Indica si el responder es local.
7. **missed_bytes**: Numero de Bytes perdidos en la conexion.
8. **orig_pkts**: Numero de paquetes enviados por el originator.
9. **orig_ip_bytes**: Numero de IP bytes enviados por el originator.
10. **resp_pkts**: Numero de paquetes enviados por el responder.
11. **resp_ip_bytes**: Numero de IP bytes enviados por el responder.
12. **conn_state_**: Varios estados de conexion:
    - **conn_state_OTH:** No se vio ningún SYN, solo tráfico en medio de la transmisión (un ejemplo de esto es una “conexión parcial” que no se cerró más tarde)
    - **conn_state_REJ:** Intento de conexión rechazado
    - **conn_state_RSTO** Conexión establecida, el originador abortó (envió un RST)
    - **conn_state_RSTOS0** El originador envió un SYN seguido de un RST, nunca vimos un SYN-ACK del respondedor
    - **conn_state_RSTR** El respondedor envió un RST
    - **conn_state_RSTRH** El respondedor envió un SYN ACK seguido de un RST, nunca vimos un SYN del (supuesto) originador
    - **conn_state_S0** Se vio un intento de conexión, no hubo respuesta.
    - **conn_state_S1** Conexión establecida, no terminada.
    - **conn_state_S2** Conexión establecida y se vio un intento de cierre por parte del originador (pero no hubo respuesta del respondedor)
    - **conn_state_S3** Conexión establecida y se vio un intento de cierre por parte del respondedor (pero no hubo respuesta del originador)
    - **conn_state_SF** Establecimiento y terminación normales. Nota que este es el mismo símbolo que para el estado S1. Puedes distinguirlos porque para S1 no habrá ningún recuento de bytes en el resumen, mientras que para SF sí lo habrá
    - **conn_state_SH** El originador envió un SYN seguido de un FIN, nunca vimos un SYN ACK del respondedor (por lo tanto, la conexión estaba “medio” abierta)
    - **conn_state_SHR**  El respondedor envió un SYN ACK seguido de un FIN, nunca vimos un SYN del originador
13. **proto_**: Protocolos usados en la conexion:
    - **proto_icmp** ICMP (Protocolo de Mensajes de Control de Internet) se utiliza principalmente para enviar mensajes de error y operacionales indicando, por ejemplo, que un servicio solicitado no está disponible o que un host o router no se puede alcanzar.
    - **proto_tcp** TCP (Protocolo de Control de Transmisión) es un protocolo de comunicación confiable que permite el envío y recepción de paquetes de datos entre dispositivos. Garantiza que los datos lleguen completos y en el mismo orden en que se transmitieron.
    - **proto_udp** UDP (Protocolo de Datagramas de Usuario) es un protocolo de comunicación más simple y rápido que TCP, pero menos confiable. Se utiliza para tareas que requieren transmisiones rápidas, como la transmisión de video o juegos en línea.
14. **service_**: Servicios asociados a la conexion:
    - **service_dhcp** DHCP (Protocolo de Configuración Dinámica de Host) es un protocolo de red que permite a los dispositivos en una red obtener su configuración de red (como la dirección IP, la máscara de subred, la puerta de enlace predeterminada, los servidores DNS, etc.) de un servidor DHCP de manera automática.
    - **service_dns** DNS (Sistema de Nombres de Dominio) es un servicio que traduce los nombres de dominio legibles por humanos (como www.google.com) en direcciones IP numéricas que las máquinas utilizan para identificar y comunicarse entre sí.
    - **service_http** HTTP (Protocolo de Transferencia de Hipertexto) es el protocolo subyacente utilizado por la World Wide Web para definir cómo se formatean y transmiten los mensajes, y qué acciones deben tomar los servidores y los navegadores en respuesta a varios comandos.
    - **service_irc** IRC (Internet Relay Chat) es un protocolo de comunicación en tiempo real que permite a las personas chatear a través de Internet. Se utiliza principalmente para el chat en grupo en salas de chat, pero también permite la comunicación uno a uno.
    - **service_other** Esta etiqueta se utiliza para clasificar cualquier tráfico que no se ajuste a ninguno de los otros servicios definidos.
    - **service_ssl** SSL (Secure Sockets Layer) es un protocolo de seguridad que proporciona comunicaciones seguras en Internet para servicios como correo electrónico, transferencia de archivos y otros datos.
    - **service_ssh** SSH (Secure Shell) es un protocolo de red que proporciona a los administradores una forma segura de acceder a una computadora a través de una red no segura. SSH también se refiere al conjunto de utilidades que implementan el protocolo.
    - **service_tcp** TCP (Protocolo de Control de Transmisión) es uno de los protocolos principales en el conjunto de protocolos de Internet. Es uno de los dos protocolos de comunicación originales utilizados en Internet y todavía se usa ampliamente hoy en día.
    - **service_udp** UDP (Protocolo de Datagramas de Usuario) es un protocolo de comunicación simple utilizado en la red de Internet. A diferencia del TCP, no proporciona las características de fiabilidad y ordenación de los paquetes de datos.
15. **multi_label**: Tipos de ataques asociados a la conexion.
    - **Attack:** esta etiqueta indica que hubo algún tipo de ataque desde el dispositivo infectado a otro host. Aquí estamos etiquetando como ataque a cualquier flujo que, al analizar su carga útil y comportamiento, intenta aprovechar algún servicio vulnerable. Por ejemplo, un ataque de fuerza bruta a algún inicio de sesión de telnet, una inyección de comandos en el encabezado de una solicitud GET, etc. 

    - ***Benign:*** esta etiqueta indica que no se encontraron actividades sospechosas o maliciosas en las conexiones. 

    - ***C&C:*** esta etiqueta indica que el dispositivo infectado estaba conectado a un servidor C&C. Esta actividad se detectó en el análisis de la captura de malware de red porque las conexiones al servidor sospechoso son periódicas o nuestro dispositivo infectado está descargando algunos binarios de él o algunas órdenes similares a IRC o decodificadas van y vienen de él. 

    - ***FileDownload:*** esta etiqueta indica que se está descargando un archivo a nuestro dispositivo infectado. Esto se detecta filtrando conexiones con bytes de respuesta superiores a 3KB o 5KB, normalmente esto se combina con algún puerto de destino sospechoso conocido o una dirección IP de destino conocida por ser un servidor C&C. 

    - ***HeartBeat:*** esta etiqueta indica que los paquetes enviados en esta conexión se utilizan para mantener un seguimiento del host infectado por el servidor C&C. Esto se detectó filtrando conexiones con bytes de respuesta inferiores a 1B y con conexiones periódicas similares, normalmente esto se combina con algún puerto de destino sospechoso conocido o una dirección IP de destino conocida por ser un servidor C&C. 

    - ***PartOfAHorizontalPortScan:*** esta etiqueta indica que las conexiones se utilizan para hacer un escaneo de puertos horizontal para recopilar información para realizar más ataques. Para poner estas etiquetas nos basamos en el patrón en el que las conexiones comparten el mismo puerto, un número similar de bytes transmitidos y múltiples direcciones IP de destino diferentes. 



La columna label especifica si es un ataque (1) o si es trafico benigno (0)

El dataset fue tomado de [Kaggle - Malware Detection in Network Traffic Data](https://www.kaggle.com/datasets/agungpambudi/network-malware-detection-connection-analysis)

