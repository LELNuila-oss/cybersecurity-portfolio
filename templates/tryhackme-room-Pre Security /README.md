# Fundamentos de Redes — Resumen y Análisis

> **Módulo:** 2 Pre-Security / Network Fundamentals  
> **Plataforma:** TryHackMe  
> **Temas:** Qué es una red, direcciones IP, direcciones MAC, ping e ICMP

---

## 1. ¿Qué es una red?

Una **red** es un conjunto de dispositivos interconectados que pueden comunicarse entre sí. En informática, una red puede estar formada por tan solo 2 dispositivos o llegar a miles de millones.

### Tipos de redes
| Tipo | Descripción |
|------|-------------|
| **Red privada** | Red interna de un hogar, empresa u organización |
| **Red pública (Internet)** | Red global que interconecta todas las redes privadas |

### El Internet
El Internet es una red gigante compuesta por muchas redes pequeñas. Su origen se remonta al proyecto **ARPANET** (finales de los años 60), financiado por el Departamento de Defensa de EE. UU. Sin embargo, el Internet tal como lo conocemos fue inventado en **1989** por **Tim Berners-Lee** con la creación de la World Wide Web (WWW).

---

## 2. Direcciones IP (Internet Protocol)

Una dirección IP permite identificar un dispositivo dentro de una red durante un período de tiempo. Está compuesta por **cuatro octetos** separados por puntos.

### Tipos de direcciones IP
| Tipo | Uso | Ejemplo |
|------|-----|---------|
| **Privada** | Identifica un dispositivo dentro de la red local | `192.168.1.77` |
| **Pública** | Identifica el dispositivo en Internet (asignada por el ISP) | `86.157.52.21` |

> Dos dispositivos en la misma red privada pueden tener la misma IP pública, ya que esta es compartida a través del router.

### IPv4 vs IPv6

| Versión | Capacidad | Formato |
|---------|-----------|---------|
| **IPv4** | 2³² (~4,290 millones de IPs) | `192.168.1.1` |
| **IPv6** | 2¹²⁸ (340+ billones de IPs) | `2001:0db8:85a3::8a2e:0370:7334` |

**¿Por qué IPv6?** La explosión de dispositivos conectados agotó el espacio de IPv4. Cisco estimó aproximadamente 50 mil millones de dispositivos conectados para finales de 2021, lo que hace esencial la transición a IPv6.

---

## 3. Direcciones MAC (Media Access Control)

La dirección MAC es un identificador único asignado de fábrica a la interfaz de red física de cada dispositivo (tarjeta de red). A diferencia de la IP, es permanente por diseño.

### Características
- Compuesta por **12 caracteres hexadecimales** separados por dos puntos.
- Ejemplo: `a4:c3:f0:85:ac:2d`
- Los **primeros 6 caracteres** identifican al fabricante.
- Los **últimos 6 caracteres** son el número único del dispositivo.

### MAC Spoofing (Suplantación de MAC)
El **MAC spoofing** es el proceso mediante el cual un dispositivo falsifica la dirección MAC de otro. Esto puede:
- Burlar controles de acceso basados en MAC (como firewalls o redes Wi-Fi de hotel).
- Ser utilizado tanto con fines legítimos (pruebas de red) como maliciosos.

**Ejemplo práctico:** Si un firewall permite tráfico solo desde la MAC del administrador, un atacante puede suplantar esa MAC para evadir el control.

> **Analogía:** La IP es como el nombre de una persona (puede cambiar), mientras que la MAC es como las huellas dactilares (única e inmutable en condiciones normales).

---

## 4. Ping e ICMP

**Ping** es una herramienta de diagnóstico de red que utiliza el protocolo **ICMP (Internet Control Message Protocol)** para medir la conectividad y el rendimiento entre dos dispositivos.

### ¿Cómo funciona?
1. El dispositivo origen envía un paquete **ICMP Echo Request** al destino.
2. El destino responde con un **ICMP Echo Reply**.
3. Se mide el tiempo de ida y vuelta (**RTT – Round Trip Time**).

### Sintaxis
```bash
ping <dirección IP o URL>

# Ejemplo:
ping 8.8.8.8
ping google.com
```

### Disponibilidad
Ping está disponible de forma nativa en **Windows**, **Linux** y **macOS**.

---

## 5. Respuestas a preguntas del módulo

| Pregunta | Respuesta |
|----------|-----------|
| ¿Qué significa "IP"? | Internet Protocol |
| ¿Cómo se llama cada sección de una dirección IP? | Octeto |
| ¿Cuántas secciones tiene una dirección IPv4? | 4 |
| ¿Qué significa "MAC"? | Media Access Control |
| ¿Qué protocolo usa ping? | ICMP |
| ¿Cuál es la sintaxis para hacer ping a 10.10.10.10? | `ping 10.10.10.10` |

---

## 6. Análisis y conceptos clave para ciberseguridad

### ¿Por qué importa esto en ciberseguridad?

1. **Identificación de dispositivos:** Comprender cómo se identifican los dispositivos (IP y MAC) es esencial para el monitoreo de redes y la detección de intrusiones.

2. **MAC Spoofing como vector de ataque:** Un atacante puede usar MAC spoofing para evadir controles de acceso basados en listas blancas. Los sistemas de seguridad no deben depender únicamente de la MAC como identificador de confianza.

3. **Gestión de IPs:** Saber distinguir entre IP pública y privada ayuda a entender el alcance de los ataques y cómo se exponen los sistemas a Internet.

4. **Ping como herramienta de reconocimiento:** Los atacantes usan ping para realizar **host discovery** durante la fase de reconocimiento. Muchas organizaciones bloquean ICMP en sus firewalls como medida defensiva.

5. **Transición IPv4 → IPv6:** La adopción de IPv6 introduce nuevas consideraciones de seguridad, como configuraciones incorrectas que pueden exponer dispositivos.

---

## Recursos adicionales

- [TryHackMe - Pre-Security Path](https://tryhackme.com/path/outline/presecurity)
- [RFC 791 - Internet Protocol](https://datatracker.ietf.org/doc/html/rfc791)
- [RFC 792 - ICMP](https://datatracker.ietf.org/doc/html/rfc792)
- [IEEE MAC Address Registry](https://regauth.standards.ieee.org/standards-ra-web/pub/view.html#registries)

# Topologías LAN, Subnetting, ARP y DHCP — Resumen y Análisis

> **Módulo:** Pre-Security / Network Fundamentals  Intro to LAN
> **Plataforma:** TryHackMe  
> **Temas:** Topologías de red, subnetting, protocolo ARP, protocolo DHCP

---

## 1. Topologías LAN (Local Area Network)

Una **topología** es el diseño o estructura física/lógica de una red. Existen tres topologías principales, cada una con ventajas y desventajas distintas.

### Comparativa general

| Topología | Costo | Escalabilidad | Redundancia | Facilidad de troubleshooting |
|-----------|-------|--------------|-------------|------------------------------|
| **Star** | Alto | Alta | Media | Media |
| **Bus** | Bajo | Baja | Muy baja | Difícil |
| **Ring** | Medio | Media | Baja | Fácil (una dirección) |

---

### Topología en Estrella (Star Topology)

Todos los dispositivos se conectan individualmente a un dispositivo central (switch o hub).

**Ventajas:**
- Alta escalabilidad: agregar dispositivos es sencillo.
- Fallo de un dispositivo no afecta al resto.
- Es la más utilizada en redes modernas.

**Desventajas:**
- Es la más costosa (requiere más cableado y hardware dedicado).
- Si el dispositivo central falla, toda la red colapsa.
- Mayor mantenimiento a medida que escala.

---

### Topología en Bus (Bus Topology)

Todos los dispositivos comparten un único cable troncal (backbone cable).

**Ventajas:**
- Fácil y económica de instalar.
- Requiere menos cableado.

**Desventajas:**
- Prone a cuellos de botella cuando múltiples dispositivos transmiten simultáneamente.
- Difícil de hacer troubleshooting.
- Sin redundancia: si el cable principal falla, toda la red se cae.

---

### Topología en Anillo (Ring Topology / Token Topology)

Los dispositivos se conectan en bucle, formando un anillo cerrado.

**Ventajas:**
- Poco cableado requerido.
- Menos dependencia de hardware dedicado.
- Fácil troubleshooting (datos viajan en una sola dirección).
- Menos propenso a cuellos de botella.

**Desventajas:**
- Ineficiente: los datos pueden tener que recorrer muchos nodos antes de llegar al destino.
- Un cable cortado o dispositivo dañado tumba toda la red.

---

### Switches vs Hubs

| Dispositivo | Comportamiento | Eficiencia |
|-------------|---------------|------------|
| **Hub** | Repite el paquete a TODOS los puertos | Baja |
| **Switch** | Envía el paquete SOLO al puerto destino | Alta |

Los switches mantienen un registro de qué dispositivo está conectado en qué puerto, reduciendo el tráfico innecesario.

**Puertos disponibles en switches:** 4, 8, 16, 24, 32 y 64 puertos.

---

### Routers

Un **router** conecta redes distintas entre sí y gestiona el paso de datos entre ellas mediante **routing** (enrutamiento).

- Pueden conectarse entre sí y con switches para agregar **redundancia**.
- Si un camino falla, los datos pueden tomar otra ruta alternativa.
- Esto evita tiempo de inactividad a costa de una leve reducción de rendimiento.

---

## 2. Subnetting

El **subnetting** es la técnica de dividir una red en subredes más pequeñas. Se puede pensar como dividir un pastel: hay una cantidad limitada de direcciones IP y el subnetting decide cómo se distribuyen.

### ¿Por qué usar subnetting?

- **Eficiencia:** Reduce el tráfico de broadcast.
- **Seguridad:** Aísla segmentos de red (ej: empleados vs. clientes en un café).
- **Control total:** Los administradores asignan recursos según necesidades.

### Estructura de una subred

Una **máscara de subred (subnet mask)** tiene la misma estructura que una IP: 4 octetos de 8 bits cada uno, con valores entre 0 y 255.

### Usos de las direcciones IP en una subred

| Tipo | Propósito | Ejemplo |
|------|-----------|---------|
| **Network Address** | Identifica el inicio de la red | `192.168.1.0` |
| **Host Address** | Identifica un dispositivo específico dentro de la red | `192.168.1.100` |
| **Default Gateway** | Dispositivo responsable de enviar datos a otras redes | `192.168.1.254` |

> El **Default Gateway** generalmente usa la primera (`.1`) o la última (`.254`) dirección de host disponible en la subred.

### Ejemplo práctico

Una cafetería puede tener dos subredes separadas:
- `192.168.1.0/24` → Red interna de empleados y cajas registradoras.
- `192.168.2.0/24` → Red pública para clientes (hotspot).

Esto mantiene la seguridad interna sin perder conectividad a Internet en ambas.

---

## 3. ARP (Address Resolution Protocol)

El **ARP** es el protocolo responsable de asociar una **dirección IP** (identificador lógico) con una **dirección MAC** (identificador físico) dentro de una red.

### ¿Cómo funciona ARP?

Cada dispositivo mantiene una tabla llamada **ARP cache**, donde almacena las asociaciones IP ↔ MAC de los dispositivos con los que se ha comunicado.

#### Proceso de resolución

```
Dispositivo A quiere comunicarse con 192.168.1.50
       │
       ▼
[ARP Request] → Broadcast a toda la red:
"¿Quién tiene la IP 192.168.1.50? Dime tu MAC."
       │
       ▼
Dispositivo con IP 192.168.1.50 responde:
[ARP Reply] → "Yo tengo esa IP, mi MAC es aa:bb:cc:dd:ee:ff"
       │
       ▼
Dispositivo A guarda la asociación en su ARP cache.
```

### Tipos de mensajes ARP

| Mensaje | Dirección | Descripción |
|---------|-----------|-------------|
| **ARP Request** | Broadcast (toda la red) | Pregunta qué dispositivo tiene una IP específica |
| **ARP Reply** | Unicast (solo al solicitante) | Responde con su dirección MAC |

### Relevancia en ciberseguridad

El **ARP Spoofing** (o ARP Poisoning) es un ataque donde un dispositivo malicioso envía respuestas ARP falsas para asociar su MAC con la IP de otro dispositivo legítimo (como el gateway). Esto permite ataques de tipo **Man-in-the-Middle (MitM)**.

---

## 4. DHCP (Dynamic Host Configuration Protocol)

El **DHCP** es el protocolo que asigna automáticamente direcciones IP a los dispositivos cuando se conectan a una red, eliminando la necesidad de configuración manual.

### Proceso DORA

El proceso de asignación de IP sigue 4 pasos conocidos como **DORA**:

```
Dispositivo              Servidor DHCP
    │                          │
    │──── DHCP Discover ──────>│  "¿Hay algún servidor DHCP en la red?"
    │                          │
    │<─── DHCP Offer ──────────│  "Puedes usar la IP 192.168.1.105"
    │                          │
    │──── DHCP Request ───────>│  "Acepto esa IP, la quiero para mí"
    │                          │
    │<─── DHCP ACK ────────────│  "Confirmado, la IP es tuya"
    │                          │
```

### Descripción de cada paquete

| Paquete | Origen | Descripción |
|---------|--------|-------------|
| **DHCP Discover** | Dispositivo → Red | Busca si existe un servidor DHCP disponible |
| **DHCP Offer** | Servidor → Dispositivo | Ofrece una dirección IP disponible |
| **DHCP Request** | Dispositivo → Servidor | Confirma que acepta la IP ofrecida |
| **DHCP ACK** | Servidor → Dispositivo | Confirma la asignación definitiva |

### IP manual vs. IP dinámica

| Método | Ventaja | Desventaja |
|--------|---------|------------|
| **Manual (estática)** | IP fija y predecible | Configuración por dispositivo |
| **Dinámica (DHCP)** | Asignación automática | IP puede cambiar con el tiempo |

> Los servidores, impresoras y dispositivos críticos suelen usar IPs estáticas. Los equipos de usuario final generalmente usan DHCP.

---

## 5. Respuestas a preguntas del módulo

### Topologías LAN
| Pregunta | Respuesta |
|----------|-----------|
| ¿Qué significa LAN? | Local Area Network |
| ¿Qué verbo describe el trabajo de los routers? | Routing |
| ¿Qué dispositivo conecta múltiples dispositivos y envía datos al destino correcto? | Switch |
| ¿Qué topología es económica de configurar? | Bus Topology |
| ¿Qué topología es costosa de configurar y mantener? | Star Topology |

### Subnetting
| Pregunta | Respuesta |
|----------|-----------|
| Término técnico para dividir una red en partes más pequeñas | Subnetting |
| ¿Cuántos bits tiene una máscara de subred? | 32 |
| ¿Cuál es el rango de un octeto de la máscara? | 0-255 |
| ¿Qué dirección identifica el inicio de una red? | Network Address |
| ¿Qué dirección identifica dispositivos dentro de la red? | Host Address |
| ¿Qué dispositivo envía datos a otra red? | Default Gateway |

### ARP
| Pregunta | Respuesta |
|----------|-----------|
| ¿Qué significa ARP? | Address Resolution Protocol |
| ¿Qué paquete ARP pregunta por una IP específica? | ARP Request |
| ¿Qué dirección es el identificador físico de un dispositivo? | MAC Address |
| ¿Qué dirección es el identificador lógico de un dispositivo? | IP Address |

### DHCP
| Pregunta | Respuesta |
|----------|-----------|
| ¿Qué paquete DHCP usa un dispositivo para obtener una IP? | DHCP Discover |
| ¿Qué paquete envía el dispositivo al aceptar la IP ofrecida? | DHCP Request |
| ¿Cuál es el último paquete enviado por el servidor DHCP? | DHCP ACK |

---

## 6. Análisis y conceptos clave para ciberseguridad

1. **Topologías como superficie de ataque:** Cada topología tiene un punto de fallo diferente. En una red en estrella, comprometer el switch central compromete toda la red. En anillo o bus, un solo punto físico puede tumbar la comunicación.

2. **ARP Spoofing / ARP Poisoning:** Al no tener autenticación, ARP es vulnerable a ataques donde un actor malicioso asocia su MAC con la IP del gateway, interceptando todo el tráfico (MitM).

3. **DHCP Starvation y Rogue DHCP:** Un atacante puede agotar el pool de IPs del servidor DHCP legítimo (DHCP Starvation) y luego poner un servidor DHCP falso (Rogue DHCP) que asigne IPs con un gateway controlado por el atacante.

4. **Segmentación por subnetting como defensa:** Separar redes (empleados, invitados, IoT) mediante subnetting limita el alcance de un ataque; un dispositivo comprometido en una subred no puede alcanzar directamente dispositivos en otra.

5. **Switches vs. Hubs en seguridad:** Los hubs retransmiten a todos los puertos, facilitando el sniffing pasivo. Los switches reducen este riesgo, aunque con técnicas como MAC flooding se puede forzar a un switch a comportarse como hub.

---

# Modelo OSI y Protocolos de Transporte (TCP/UDP) — Resumen y Análisis

> **Módulo:** Pre-Security / Network Fundamentals  
> **Plataforma:** TryHackMe  
> **Temas:** Modelo OSI (7 capas), protocolo TCP, protocolo UDP

---

## 1. ¿Qué es el Modelo OSI?

El **OSI (Open Systems Interconnection) Model** es un modelo conceptual esencial en redes que proporciona un marco estándar para que todos los dispositivos en una red puedan enviar, recibir e interpretar datos de forma uniforme, independientemente de su diseño o fabricante.

### Características principales
- Compuesto por **7 capas**, numeradas del 1 al 7.
- Cada capa tiene responsabilidades específicas.
- El proceso de agregar información a los datos al recorrer las capas se llama **encapsulación**.
- Permite que dispositivos con distintas funciones se comuniquen usando un lenguaje común.

### Diagrama del modelo OSI

```
┌─────────────────────────────────┐
│  Capa 7 │  Application          │  ← Interfaz con el usuario
├─────────────────────────────────┤
│  Capa 6 │  Presentation         │  ← Traducción y cifrado
├─────────────────────────────────┤
│  Capa 5 │  Session              │  ← Gestión de sesiones
├─────────────────────────────────┤
│  Capa 4 │  Transport            │  ← TCP / UDP
├─────────────────────────────────┤
│  Capa 3 │  Network              │  ← Routing (IP)
├─────────────────────────────────┤
│  Capa 2 │  Data Link            │  ← Direccionamiento MAC
├─────────────────────────────────┤
│  Capa 1 │  Physical             │  ← Señales eléctricas, cables
└─────────────────────────────────┘
```

> **Tip para memorizar (de abajo a arriba):** _"Please Do Not Throw Sausage Pizza Away"_  
> Physical → Data Link → Network → Transport → Session → Presentation → Application

---

## 2. Las 7 Capas del Modelo OSI

---

### Capa 1 — Physical (Física)

La capa más baja del modelo. Se encarga de la transmisión de datos a través de señales eléctricas entre dispositivos físicos.

- Los datos se representan en sistema binario: **1s y 0s**.
- Incluye el hardware de red: cables, conectores, tarjetas de red.
- Ejemplo: cables **Ethernet** conectando dispositivos.

---

### Capa 2 — Data Link (Enlace de Datos)

Se encarga del **direccionamiento físico** de la transmisión.

- Recibe el paquete de la capa de Red (que incluye la IP) y añade la **dirección MAC** del dispositivo destino.
- Cada dispositivo de red tiene una **NIC (Network Interface Card)** con una dirección MAC única, asignada por el fabricante y "quemada" en el hardware.
- También presenta los datos en un formato adecuado para su transmisión.
- Las MACs pueden ser falsificadas (**spoofed**), aunque no se pueden cambiar permanentemente.

---

### Capa 3 — Network (Red)

Capa donde ocurre el **routing** (enrutamiento) y el reensamblado de datos.

- Opera con **direcciones IP** (ej: `192.168.1.100`).
- Determina el **camino óptimo** para enviar los paquetes de datos.
- Los routers son dispositivos de **Capa 3**.

#### Protocolos de enrutamiento

| Protocolo | Nombre completo | Función |
|-----------|----------------|---------|
| **OSPF** | Open Shortest Path First | Elige la ruta más corta y eficiente |
| **RIP** | Routing Information Protocol | Elige rutas basándose en número de saltos |

#### Factores que determinan la ruta óptima
- **Ruta más corta:** menor número de dispositivos intermedios.
- **Ruta más confiable:** historial de pérdida de paquetes.
- **Conexión más rápida:** fibra óptica vs. cobre.

---

### Capa 4 — Transport (Transporte)

Capa encargada de la transmisión de datos entre dispositivos usando dos protocolos principales: **TCP** y **UDP** (detallados en la sección 3).

---

### Capa 5 — Session (Sesión)

Una vez que los datos están formateados (desde la capa 6), la capa de sesión crea y mantiene la **conexión** con el dispositivo destino.

- Al establecerse la conexión, se crea una **sesión**.
- Cierra la conexión si no ha sido utilizada o si se pierde.
- Implementa **checkpoints**: si los datos se pierden, solo se reenvían los fragmentos más recientes (ahorra ancho de banda).
- Las sesiones son **únicas**: los datos no viajan entre sesiones distintas.

---

### Capa 6 — Presentation (Presentación)

Capa donde comienza la **estandarización** de los datos.

- Actúa como **traductor** entre la capa de aplicación (7) y el resto del modelo.
- Garantiza que los datos se presenten de forma consistente sin importar el software usado.
- Ejemplo: dos usuarios con clientes de correo distintos ven el mismo contenido del email.
- Aquí ocurre el **cifrado de datos** (ej: HTTPS al visitar un sitio seguro).

---

### Capa 7 — Application (Aplicación)

La capa más cercana al usuario final.

- Define los **protocolos y reglas** para interactuar con los datos enviados/recibidos.
- Proporciona interfaces gráficas (**GUI**) en aplicaciones cotidianas: navegadores, clientes de correo, exploradores de archivos.
- Incluye protocolos como **DNS (Domain Name System)**, que traduce nombres de dominio (google.com) a direcciones IP.

---

## 3. TCP vs. UDP — Capa de Transporte

### TCP (Transmission Control Protocol)

Protocolo orientado a la **confiabilidad y garantía** de entrega de datos.

- Establece una **conexión constante** entre dispositivos durante toda la transferencia.
- Incorpora **verificación de errores (error checking)**.
- Garantiza que los paquetes lleguen **en el orden correcto**.

| Ventajas | Desventajas |
|----------|-------------|
| Garantiza exactitud de los datos | Requiere conexión confiable |
| Sincroniza dispositivos para evitar saturación | Una conexión lenta puede crear cuello de botella |
| Control total del proceso de transmisión | Más lento que UDP por los procesos adicionales |

**Casos de uso:** transferencia de archivos, navegación web, correo electrónico.

---

### UDP (User Datagram Protocol)

Protocolo orientado a la **velocidad**, sin garantía de entrega.

- No establece conexión previa ni verifica si los datos llegaron.
- El principio es: "envía y espera lo mejor".
- Sin sincronización entre dispositivos.

| Ventajas | Desventajas |
|----------|-------------|
| Mucho más rápido que TCP | No verifica si los datos llegaron |
| No reserva conexión continua | Conexiones inestables generan mala experiencia |
| Flexible para el desarrollador de software | Sin control de orden de paquetes |

**Casos de uso:** streaming de video, videollamadas, protocolos de descubrimiento de red (ARP, DHCP).

---

### Comparativa directa TCP vs. UDP

| Característica | TCP | UDP |
|---------------|-----|-----|
| Confiabilidad | Alta | Ninguna |
| Velocidad | Media | Alta |
| Orden de paquetes | Garantizado | No garantizado |
| Verificación de errores | Sí | No |
| Conexión previa | Sí (three-way handshake) | No |
| Uso típico | Email, web, archivos | Video, juegos, DNS |

---

## 4. Respuestas a preguntas del módulo

### Modelo OSI General
| Pregunta | Respuesta |
|----------|-----------|
| ¿Qué significa "OSI"? | Open Systems Interconnection |
| ¿Cuántas capas tiene el modelo OSI? | 7 |
| ¿Qué término describe cuando se agrega información a los datos? | Encapsulation |

### Capa 1 — Physical
| Pregunta | Respuesta |
|----------|-----------|
| Nombre de la capa | Physical |
| Sistema numérico de 0s y 1s | Binary (binario) |
| Cables usados para conectar dispositivos | Ethernet cables |

### Capa 2 — Data Link
| Pregunta | Respuesta |
|----------|-----------|
| Nombre de la capa | Data Link |
| Hardware de red presente en todos los dispositivos | Network Interface Card (NIC) |

### Capa 3 — Network
| Pregunta | Respuesta |
|----------|-----------|
| Nombre de la capa | Network |
| ¿Los paquetes toman siempre la ruta óptima? | Y |
| ¿Qué significa OSPF? | Open Shortest Path First |
| ¿Qué significa RIP? | Routing Information Protocol |
| ¿Qué tipo de direcciones maneja esta capa? | IP Addresses |

### Capa 4 — Transport
| Pregunta | Respuesta |
|----------|-----------|
| Nombre de la capa | Transport |
| ¿Qué significa TCP? | Transmission Control Protocol |
| ¿Qué significa UDP? | User Datagram Protocol |
| ¿Qué protocolo garantiza exactitud de datos? | TCP |
| ¿Qué protocolo no verifica si los datos llegaron? | UDP |
| ¿Qué protocolo usa un cliente de email? | TCP |
| ¿Qué protocolo usa una app de descarga de archivos? | TCP |
| ¿Qué protocolo usa una app de streaming de video? | UDP |

### Capa 5 — Session
| Pregunta | Respuesta |
|----------|-----------|
| Nombre de la capa | Session |
| Término técnico para cuando se establece una conexión | Session |

### Capa 6 — Presentation
| Pregunta | Respuesta |
|----------|-----------|
| Nombre de la capa | Presentation |
| Propósito principal de esta capa | Translator (Traductor) |

### Capa 7 — Application
| Pregunta | Respuesta |
|----------|-----------|
| Nombre de la capa | Application |
| Término técnico para el software con el que interactúan los usuarios | Graphical User Interface (GUI) |

---

## 5. Análisis y conceptos clave para ciberseguridad

1. **Ataques por capa:** Conocer el modelo OSI permite identificar en qué capa ocurre un ataque. Por ejemplo, un ataque de ARP Spoofing opera en la **Capa 2**, mientras que un ataque DDoS puede afectar la **Capa 4** (inundando TCP connections) o la **Capa 7** (HTTP flood).

2. **Cifrado en Capa 6:** HTTPS opera en la capa de presentación. Un sitio sin HTTPS expone los datos en texto plano, siendo vulnerable a sniffing en redes no confiables.

3. **TCP SYN Flood:** Aprovecha el proceso de handshake de TCP enviando masivas solicitudes de conexión sin completarlas, agotando los recursos del servidor. Es un ataque clásico de denegación de servicio (DoS).

4. **UDP y amplificación DNS:** UDP es usado en ataques de amplificación porque permite enviar paquetes con IP de origen falsificada. El atacante envía una pequeña consulta DNS (UDP) y la respuesta (mucho mayor) se dirige a la víctima.

5. **Encapsulación como concepto de análisis forense:** Al analizar tráfico de red (ej: con Wireshark), entender la encapsulación del modelo OSI permite diseccionar un paquete capa por capa para identificar indicadores de compromiso (IoCs).

---


# Packets & Frames, TCP/IP, UDP y Puertos — Resumen y Análisis

> **Módulo:** Pre-Security / Network Fundamentals  
> **Plataforma:** TryHackMe  
> **Temas:** Paquetes y frames, Three-way handshake, modelo TCP/IP, UDP, puertos comunes

---

## 1. Packets y Frames

### ¿Qué son?

Los **paquetes** y **frames** son pequeñas piezas de datos que, al ensamblarse, forman un mensaje completo. Aunque ambos transportan datos, operan en capas distintas del modelo OSI.

| Concepto | Capa OSI | Contiene | Identificador |
|----------|----------|----------|---------------|
| **Frame** | Capa 2 — Data Link | Encapsula el paquete + direcciones MAC | MAC Address |
| **Packet** | Capa 3 — Network | Datos + cabecera IP (IP header + payload) | IP Address |

> **Analogía:** Un frame es el sobre (envelope), y el paquete es la carta (letter) dentro del sobre. El sobre indica cómo mover el contenido; la carta indica cómo procesarlo al llegar.

### ¿Por qué usar paquetes?

Enviar datos en pequeñas piezas en lugar de un bloque completo reduce el riesgo de cuellos de botella. Por ejemplo, al cargar una imagen desde un sitio web, esta llega dividida en múltiples paquetes que el dispositivo receptor reensambla.

---

### Cabeceras (Headers) de un paquete IP

| Header | Descripción |
|--------|-------------|
| **Time to Live (TTL)** | Temporizador de expiración del paquete. Evita que paquetes perdidos saturen la red indefinidamente |
| **Checksum** | Valor para verificar la integridad de los datos. Si cambia algún byte, el checksum no coincide → paquete corrupto |
| **Source Address** | Dirección IP del dispositivo origen |
| **Destination Address** | Dirección IP del dispositivo destino |

---

## 2. El Modelo TCP/IP

El modelo **TCP/IP** es una versión simplificada del modelo OSI, compuesta por **4 capas**:

```
┌────────────────────────┐
│  Application           │  ← Equivale a capas 5, 6, 7 del OSI
├────────────────────────┤
│  Transport             │  ← TCP / UDP (Capa 4 OSI)
├────────────────────────┤
│  Internet              │  ← Routing, IP (Capa 3 OSI)
├────────────────────────┤
│  Network Interface     │  ← MAC, frames (Capas 1 y 2 OSI)
└────────────────────────┘
```

Al igual que el OSI, la información se agrega en cada capa al recorrerlas (**encapsulación**), y se elimina al recibirlas (**desencapsulación**).

---

## 3. TCP — Three-Way Handshake

TCP es un protocolo **orientado a la conexión**: antes de enviar cualquier dato, se debe establecer una conexión entre cliente y servidor. Este proceso se llama **Three-Way Handshake**.

### Cabeceras de un paquete TCP

| Header | Descripción |
|--------|-------------|
| **Source Port** | Puerto de origen (elegido aleatoriamente entre 0–65535) |
| **Destination Port** | Puerto destino del servicio en el servidor (no aleatorio, ej: 80 para HTTP) |
| **Source IP** | IP del dispositivo que envía |
| **Destination IP** | IP del dispositivo destino |
| **Sequence Number** | Número aleatorio asignado al primer fragmento de datos |
| **Acknowledgement Number** | Sequence Number + 1 del fragmento recibido |
| **Checksum** | Garantiza integridad: si el resultado matemático no coincide, el dato está corrupto |
| **Data** | Bytes del archivo o mensaje que se está transmitiendo |
| **Flag** | Indica cómo debe manejarse el paquete (SYN, ACK, FIN, RST, etc.) |

---

### Proceso del Three-Way Handshake

```
   Cliente                          Servidor
      │                                 │
      │──────── SYN (ISN=0) ──────────>│  "Quiero conectarme, mi ISN es 0"
      │                                 │
      │<── SYN/ACK (ISN=5000, ACK=0) ──│  "Acepto, mi ISN es 5000, confirmo tu 0"
      │                                 │
      │──────── ACK (ISN+1=1) ────────>│  "Confirmo tu ISN de 5000, aquí van datos"
      │                                 │
      │<════════ DATA ════════════════>│  ← Transferencia de datos
      │                                 │
      │──────── FIN ──────────────────>│  "Quiero cerrar la conexión"
      │                                 │
      │<──────── FIN/ACK ──────────────│  "Recibido, yo también cierro"
      │                                 │
      │──────── ACK ──────────────────>│  "Confirmado"
```

### Tabla de mensajes TCP

| Paso | Mensaje | Descripción |
|------|---------|-------------|
| 1 | **SYN** | El cliente inicia la conexión y sincroniza números de secuencia |
| 2 | **SYN/ACK** | El servidor confirma la sincronización del cliente |
| 3 | **ACK** | El cliente confirma la recepción; conexión establecida |
| 4 | **DATA** | Se transmiten los datos |
| 5 | **FIN** | Cierre ordenado de la conexión |
| — | **RST** | Cierre abrupto por error o fallo del sistema |

### Números de secuencia (Sequence Numbers)

| Dispositivo | ISN inicial | Siguiente |
|-------------|-------------|-----------|
| Cliente | 0 | 0 + 1 = 1 |
| Cliente | 1 | 1 + 1 = 2 |
| Cliente | 2 | 2 + 1 = 3 |

Ambos dispositivos deben acordar la misma secuencia numérica para que los datos lleguen en el orden correcto.

---

## 4. UDP/IP

El **UDP (User Datagram Protocol)** es un protocolo **sin estado (stateless)**: no requiere conexión previa ni sincronización entre dispositivos. No hay Three-Way Handshake.

### Cabeceras de un paquete UDP

| Header | Descripción |
|--------|-------------|
| **Time to Live (TTL)** | Expiración del paquete para no saturar la red |
| **Source Address** | IP del dispositivo origen |
| **Destination Address** | IP del dispositivo destino |
| **Source Port** | Puerto de origen (elegido aleatoriamente) |
| **Destination Port** | Puerto del servicio destino (no aleatorio) |
| **Data** | Bytes del archivo o mensaje transmitido |

### Comparativa TCP vs. UDP

| Característica | TCP | UDP |
|---------------|-----|-----|
| Tipo de conexión | Con estado (stateful) | Sin estado (stateless) |
| Handshake | Three-Way Handshake | Ninguno |
| Garantía de entrega | Sí | No |
| Verificación de integridad | Checksum completo | Básico |
| Velocidad | Más lento | Más rápido |
| Uso típico | Archivos, web, email | Video, voz, DNS, juegos |

---

## 5. Puertos

Los **puertos** son puntos de intercambio de datos numerados entre **0 y 65535**. Permiten que múltiples aplicaciones usen la red simultáneamente en el mismo dispositivo, cada una en su propio puerto.

> **Analogía:** Un puerto en red es como un muelle en un puerto marítimo: cada tipo de embarcación (protocolo/aplicación) tiene un muelle (puerto) asignado.

### Puertos comunes (0–1024)

| Protocolo | Puerto | Descripción |
|-----------|--------|-------------|
| **FTP** (File Transfer Protocol) | 21 | Transferencia de archivos en modelo cliente-servidor |
| **SSH** (Secure Shell) | 22 | Acceso remoto seguro vía interfaz de texto |
| **HTTP** (HyperText Transfer Protocol) | 80 | Navegación web estándar |
| **HTTPS** (HTTP Secure) | 443 | Navegación web cifrada (TLS/SSL) |
| **SMB** (Server Message Block) | 445 | Compartir archivos e impresoras en red |
| **RDP** (Remote Desktop Protocol) | 3389 | Acceso remoto con interfaz gráfica |

> **Nota:** Los protocolos pueden ejecutarse en puertos no estándar (ej: servidor web en puerto 8080 en lugar del 80). En ese caso se especifica como `ip:puerto` → `192.168.1.1:8080`.

---

## 6. Respuestas a preguntas del módulo

### Packets & Frames
| Pregunta | Respuesta |
|----------|-----------|
| ¿Cómo se llama un dato que tiene información IP? | Packet |
| ¿Cómo se llama un dato que NO tiene información IP? | Frame |

### TCP / Three-Way Handshake
| Pregunta | Respuesta |
|----------|-----------|
| ¿Qué header de TCP garantiza la integridad de los datos? | Checksum |
| Orden del Three-Way Handshake | SYN, SYN/ACK, ACK |

### UDP
| Pregunta | Respuesta |
|----------|-----------|
| ¿Qué significa UDP? | User Datagram Protocol |
| ¿Qué tipo de conexión es UDP? | Stateless (sin estado) |
| ¿Qué protocolo usarías para transferir un archivo? | TCP |
| ¿Qué protocolo usarías para una videollamada? | UDP |

### Puertos
| Pregunta | Respuesta |
|----------|-----------|
| Flag del reto de conexión a puerto | `THM{YOU_CONNECTED_TO_A_PORT}` |

---

## 7. Análisis y conceptos clave para ciberseguridad

1. **TTL como herramienta de reconocimiento:** El campo TTL en los paquetes puede revelar el sistema operativo del dispositivo origen. Windows suele iniciar TTL en 128; Linux/Unix en 64. Esto es útil tanto para administradores como para atacantes en la fase de fingerprinting.

2. **RST Injection (TCP Reset Attack):** Un atacante puede enviar paquetes RST falsificados para terminar abruptamente conexiones TCP activas entre dos dispositivos, causando una denegación de servicio en la capa de transporte.

3. **Port Scanning:** Herramientas como **Nmap** envían paquetes a múltiples puertos para determinar cuáles están abiertos, cerrados o filtrados. Conocer los puertos estándar es fundamental para interpretar los resultados de un escaneo.

4. **Puertos no estándar como técnica de evasión:** Los atacantes frecuentemente ejecutan servicios maliciosos (C2 servers, backdoors) en puertos inusuales para evadir firewalls configurados para bloquear solo los puertos estándar.

5. **UDP Flood (DDoS):** Al no requerir handshake, UDP es fácilmente explotable para ataques de inundación. El atacante envía masivos paquetes UDP a puertos aleatorios, obligando al servidor a responder con mensajes ICMP "puerto inalcanzable", saturando los recursos.

6. **SMB y RDP como vectores críticos:** Los puertos 445 (SMB) y 3389 (RDP) expuestos a Internet son objetivos frecuentes. EternalBlue (WannaCry) explotó SMB; ataques de fuerza bruta son comunes contra RDP.

---

# Extendiendo la Red — Port Forwarding, Firewalls, VPN y Dispositivos LAN

> **Módulo:** Pre-Security / Network Fundamentals  
> **Plataforma:** TryHackMe  
> **Temas:** Port Forwarding, Firewalls, VPN, Routers, Switches, VLANs

---

## 1. Port Forwarding (Reenvío de Puertos)

El **port forwarding** es un mecanismo esencial para hacer que aplicaciones y servicios sean accesibles desde Internet. Sin él, los servicios solo son visibles dentro de la red local (**intranet**).

### ¿Cómo funciona?

Sin port forwarding, un servidor web en `192.168.1.10:80` solo es accesible para dispositivos de la misma red local. Con port forwarding configurado en el router, ese mismo servidor puede ser alcanzado desde Internet a través de la IP pública del router.

```
Sin Port Forwarding:
  [PC-A] ──┐
           ├── [Router 192.168.1.1 / IP pública: 82.62.51.70]  ✗ Internet no puede entrar
  [PC-B] ──┘   [Servidor: 192.168.1.10:80]

Con Port Forwarding:
  [Internet] ──> 82.62.51.70:80 ──> [Router] ──> 192.168.1.10:80  ✓
```

### Puntos clave

- Se configura en el **router** de la red.
- Abre puertos específicos para redirigir tráfico entrante a un dispositivo interno.
- No es lo mismo que un firewall: el port forwarding **abre** puertos; el firewall **controla** si el tráfico puede pasar por ellos.

---

## 2. Firewalls

Un **firewall** es un dispositivo (o software) responsable de determinar qué tráfico puede entrar o salir de una red. Actúa como seguridad fronteriza de la red.

### Criterios de filtrado

Un firewall toma decisiones basándose en:

| Criterio | Ejemplo |
|----------|---------|
| **Origen del tráfico** | ¿Viene de una red confiable o sospechosa? |
| **Destino del tráfico** | ¿Va a una red permitida? |
| **Puerto de destino** | ¿Es tráfico al puerto 80 (HTTP)? |
| **Protocolo usado** | ¿Es TCP, UDP o ambos? |

### Tipos de Firewalls

| Tipo | Descripción | Ventajas | Desventajas |
|------|-------------|----------|-------------|
| **Stateful** | Analiza la conexión completa (no solo paquetes individuales). Toma decisiones dinámicas basadas en el comportamiento total del host. | Detección más inteligente; puede bloquear dispositivos enteros | Consume más recursos del sistema |
| **Stateless** | Usa reglas estáticas para evaluar paquetes individuales. Un paquete malo no implica bloqueo del dispositivo. | Usa menos recursos; efectivo contra ataques DDoS | "Dumb firewall": solo funciona si las reglas están bien definidas |

### Capas OSI donde operan los firewalls

Los firewalls operan principalmente en las **Capas 3 y 4** del modelo OSI:
- **Capa 3 (Network):** Filtrado por dirección IP.
- **Capa 4 (Transport):** Filtrado por puerto y protocolo (TCP/UDP).

Firewalls más avanzados (NGFW) también operan en Capa 7 (Application).

---

## 3. VPN (Virtual Private Network)

Una **VPN** es una tecnología que permite que dispositivos en redes separadas se comuniquen de forma segura creando un **túnel cifrado** a través de Internet.

### ¿Cómo funciona?

Los dispositivos conectados a través de VPN forman su propia red privada virtual, aunque estén físicamente en ubicaciones distintas.

```
[Oficina #1 - Red 192.168.1.0/24] ──────┐
                                         ├─── Túnel VPN cifrado ─── [Red #3 Virtual]
[Oficina #2 - Red 192.168.2.0/24] ──────┘
```

### Beneficios de una VPN

| Beneficio | Descripción |
|-----------|-------------|
| **Conexión geográfica** | Une redes de distintas ubicaciones físicas (ej: sucursales de empresa) |
| **Privacidad** | Cifra los datos; no pueden ser interceptados en redes públicas (WiFi de café) |
| **Anonimato** | Oculta el tráfico del ISP y otros intermediarios; útil para periodistas y activistas |

> **Nota:** El nivel de anonimato depende de la política de registros (logs) del proveedor VPN. Una VPN que registra actividad equivale a no usar VPN.

### Tecnologías VPN

| Tecnología | Descripción | Características |
|------------|-------------|-----------------|
| **PPP** | Protocolo base de autenticación y cifrado. Usa par de clave privada/certificado público | No enrutable por sí solo |
| **PPTP** | Point-to-Point Tunneling Protocol. Permite que PPP salga de la red | Fácil de configurar; cifrado débil |
| **IPSec** | Internet Protocol Security. Cifra datos sobre el framework IP existente | Difícil de configurar; cifrado fuerte; amplio soporte |

---

## 4. Dispositivos de Red LAN

### Router

El **router** conecta redes distintas y gestiona el paso de datos entre ellas mediante **routing** (enrutamiento).

- Opera en la **Capa 3 (Network)** del modelo OSI.
- Determina la ruta óptima para los paquetes según:
  - Ruta más corta (menos saltos).
  - Ruta más confiable (menor pérdida de paquetes histórica).
  - Medio más rápido (fibra vs. cobre).
- Suele incluir interfaz de administración para configurar port forwarding, firewalls, etc.
- Es un dispositivo dedicado; no realiza las funciones de un switch.

---

### Switch

Un **switch** es un dispositivo dedicado a conectar múltiples dispositivos dentro de una red local, usando cables Ethernet. Puede conectar de 3 a 63 dispositivos.

#### Switch Capa 2 (Data Link)

- Reenvía **frames** a dispositivos usando su **dirección MAC**.
- Solo responsable de entregar datos al dispositivo correcto dentro de la red local.

#### Switch Capa 3 (Network)

- Más sofisticado: puede realizar funciones de un router.
- Reenvía frames (como Capa 2) **y** enruta paquetes usando el protocolo IP.
- Permite crear **VLANs**.

#### Comparativa de switches

| Característica | Switch Capa 2 | Switch Capa 3 |
|---------------|--------------|--------------|
| Reenvío por MAC | Sí | Sí |
| Enrutamiento IP | No | Sí |
| VLANs | Sí | Sí |
| Complejidad | Básica | Avanzada |

---

### VLAN (Virtual Local Area Network)

Una **VLAN** permite dividir virtualmente dispositivos dentro de la misma red física en segmentos separados con reglas de comunicación propias.

```
                     [Switch Capa 3]
                      /            \
          [VLAN: Ventas]        [VLAN: Contabilidad]
          192.168.1.0/24        192.168.2.0/24
          PC-Vendedor1          PC-Contador1
          PC-Vendedor2          PC-Contador2

→ Ambas VLANs acceden a Internet.
→ Ventas NO puede comunicarse con Contabilidad directamente.
```

**Beneficio principal:** Segmentación de red para mayor seguridad sin necesidad de hardware adicional.

---

## 5. Respuestas a preguntas del módulo

### Port Forwarding
| Pregunta | Respuesta |
|----------|-----------|
| ¿Qué dispositivo configura el port forwarding? | Router |

### Firewalls
| Pregunta | Respuesta |
|----------|-----------|
| ¿En qué capas OSI operan los firewalls? | 3 & 4 |
| ¿Qué tipo de firewall inspecciona la conexión completa? | Stateful |
| ¿Qué tipo de firewall inspecciona paquetes individuales? | Stateless |

### VPN
| Pregunta | Respuesta |
|----------|-----------|
| ¿Qué tecnología VPN solo cifra y autentica datos? | PPP |
| ¿Qué tecnología VPN usa el framework IP? | IPSec |

### Dispositivos LAN
| Pregunta | Respuesta |
|----------|-----------|
| ¿Cuál es el verbo para la acción que realiza un router? | Routing |
| ¿Cuáles son las dos capas en que operan los switches? | Layer 2, Layer 3 |

---

## 6. Análisis y conceptos clave para ciberseguridad

1. **Port Forwarding como superficie de ataque:** Cada puerto abierto hacia Internet es un potencial vector de entrada. Un puerto de RDP (3389) o SMB (445) expuesto públicamente sin protección adicional es un objetivo frecuente de escaneos automatizados y ataques de fuerza bruta.

2. **Firewall Evasion:** Los atacantes usan técnicas como encapsular tráfico malicioso en protocolos permitidos (ej: túneles DNS o HTTPS) para evadir firewalls stateless que solo inspeccionan cabeceras de Capa 3/4. Los firewalls de próxima generación (NGFW) inspeccionan hasta Capa 7 para mitigar esto.

3. **VPN Split Tunneling:** Algunos proveedores VPN permiten que solo parte del tráfico pase por el túnel (split tunneling). Esto puede exponer datos sensibles si el tráfico hacia servicios críticos no se incluye en el túnel cifrado.

4. **VLAN Hopping:** Un atacante en una VLAN puede intentar enviar frames con doble etiqueta (double tagging) para saltar a otra VLAN no autorizada. Mitigación: deshabilitar el trunk automático (Dynamic Trunking Protocol) en puertos de acceso.

5. **ARP dentro de VLANs:** Aunque las VLANs separan el tráfico lógicamente, el ARP Spoofing sigue siendo posible dentro de la misma VLAN. La segmentación no elimina las amenazas internas.

6. **Stateful vs. Stateless en DDoS:** Los firewalls stateless son preferibles para mitigar DDoS volumétrico porque no mantienen estado de conexión y pueden descartar paquetes a alta velocidad. Los firewalls stateful se saturarían intentando rastrear millones de conexiones falsas.

---

## Resumen del módulo completo

| Tema | Conceptos clave |
|------|----------------|
| Redes e Internet | Red privada/pública, ARPANET, Tim Berners-Lee |
| IP y MAC | IPv4/IPv6, MAC spoofing, ping/ICMP |
| Topologías LAN | Star, Bus, Ring; Switch vs. Hub; Router |
| Subnetting | Network/Host/Gateway address, máscara de subred |
| ARP y DHCP | ARP Request/Reply, proceso DORA |
| Modelo OSI | 7 capas, encapsulación, función de cada capa |
| TCP/UDP | Three-Way Handshake, stateful vs. stateless |
| Packets y Frames | Estructura, cabeceras IP, TTL, checksum |
| Puertos | 0-65535, puertos comunes (FTP, SSH, HTTP, HTTPS, SMB, RDP) |
| Port Forwarding | Router, intranet vs. Internet |
| Firewalls | Stateful vs. Stateless, Capas 3 & 4 |
| VPN | PPP, PPTP, IPSec, túnel cifrado |
| Dispositivos LAN | Router (L3), Switch L2/L3, VLAN |

---

# DNS en Detalle — Resumen y Análisis

> **Módulo:** How The Web Works  
> **Plataforma:** TryHackMe  
> **Temas:** ¿Qué es DNS?, jerarquía de dominios, tipos de registros, flujo de una consulta DNS

---

## 1. ¿Qué es DNS?

El **DNS (Domain Name System)** es el sistema que permite comunicarse con dispositivos en Internet usando nombres legibles (como `tryhackme.com`) en lugar de direcciones IP numéricas (como `104.26.10.229`).

> **Analogía:** DNS es como la agenda de contactos del teléfono: en lugar de marcar un número de 10 dígitos, buscas el nombre de la persona y el teléfono se resuelve automáticamente.

---

## 2. Jerarquía de Dominios

Los dominios siguen una estructura jerárquica de derecha a izquierda:

```
jupiter.servers.tryhackme.com
│        │         │        │
│        │         │        └── TLD (.com)
│        │         └─────────── Second-Level Domain (tryhackme)
│        └───────────────────── Subdomain (servers)
└────────────────────────────── Subdomain (jupiter)
```

### TLD (Top-Level Domain)

La parte más a la derecha del dominio.

| Tipo | Nombre completo | Propósito | Ejemplos |
|------|----------------|-----------|---------|
| **gTLD** | Generic Top-Level Domain | Indica el propósito del dominio | `.com` (comercial), `.org` (organización), `.edu` (educación), `.gov` (gobierno) |
| **ccTLD** | Country Code Top-Level Domain | Indica el país o región | `.ca` (Canadá), `.co.uk` (Reino Unido), `.sv` (El Salvador) |

> Actualmente existen más de 2,000 TLDs disponibles, incluyendo nuevos gTLDs como `.online`, `.club`, `.website`, `.biz`.

### Second-Level Domain

La parte inmediatamente a la izquierda del TLD. En `tryhackme.com`, `tryhackme` es el Second-Level Domain.

**Restricciones:**
- Máximo **63 caracteres** + TLD.
- Solo puede contener: `a-z`, `0-9`, y guiones (`-`).
- No puede comenzar ni terminar con guión.
- No puede tener guiones consecutivos.

### Subdomain

Se ubica a la izquierda del Second-Level Domain, separado por un punto.

**Restricciones:**
- Máximo **63 caracteres** por subdomain.
- Mismas reglas de caracteres que el Second-Level Domain.
- Longitud total del dominio: máximo **253 caracteres**.
- Sin límite en la cantidad de subdominios creados.

---

## 3. Tipos de Registros DNS

| Tipo | Función | Ejemplo |
|------|---------|---------|
| **A Record** | Resuelve a una dirección **IPv4** | `tryhackme.com → 104.26.10.229` |
| **AAAA Record** | Resuelve a una dirección **IPv6** | `tryhackme.com → 2606:4700:20::681a:be5` |
| **CNAME Record** | Resuelve a **otro nombre de dominio** (alias) | `store.tryhackme.com → shops.shopify.com` |
| **MX Record** | Indica los servidores de **correo electrónico** del dominio; incluye prioridad | `tryhackme.com → alt1.aspmx.l.google.com (prioridad: 10)` |
| **TXT Record** | Almacena **texto libre**; múltiples usos | Verificación de propiedad, SPF, DMARC |

### Detalle: Registro MX

El campo de **prioridad** indica al cliente qué servidor intentar primero. Un valor numérico más bajo = mayor prioridad. Si el servidor principal falla, se intenta el siguiente en la lista.

### Detalle: Registro TXT

Usos comunes:
- **SPF (Sender Policy Framework):** lista servidores autorizados a enviar correo en nombre del dominio (combate spam).
- **DMARC:** política de autenticación de correo.
- **Verificación de propiedad:** al registrarse en servicios de terceros (ej: Google Search Console, Microsoft 365).

```
Ejemplos de registros TXT:
@ TXT "v=spf1 ip4:192.0.2.0/24 include:_spf.google.com ~all"
_dmarc.example.com TXT "v=DMARC1; p=reject; rua=mailto:reports@example.com"
@ TXT "MS=ms12345678"   ← Verificación de propiedad Microsoft
```

---

## 4. Flujo de una Consulta DNS

Cuando escribes un dominio en el navegador, ocurre lo siguiente:

```
[Usuario: tryhackme.com]
        │
        ▼
1. ¿Está en caché local del PC?
   → Sí: usa la IP guardada  ✓
   → No: continúa ↓
        │
        ▼
2. Recursive DNS Server (ISP o personalizado, ej: 8.8.8.8)
   ¿Está en su caché?
   → Sí: devuelve la respuesta  ✓
   → No: continúa ↓
        │
        ▼
3. Root DNS Server
   "El TLD es .com → te redirijo al servidor TLD de .com"
        │
        ▼
4. TLD Server (.com)
   "El dominio es tryhackme → el nameserver es kip.ns.cloudflare.com"
        │
        ▼
5. Authoritative DNS Server (Nameserver)
   Tiene los registros reales del dominio
   Devuelve: IP = 104.26.10.229  ✓
        │
        ▼
6. Recursive DNS guarda en caché (por TTL) y devuelve al usuario
```

### Servidores en el proceso

| Servidor | Función |
|----------|---------|
| **Caché local** | Almacena respuestas previas en el propio equipo |
| **Recursive DNS Server** | Intermediario que busca la respuesta; generalmente provisto por el ISP |
| **Root DNS Server** | Redirige al TLD Server correcto según la extensión del dominio |
| **TLD Server** | Conoce el nameserver autorizado para cada dominio bajo su TLD |
| **Authoritative DNS Server** | Almacena los registros DNS reales del dominio; aquí se hacen las actualizaciones |

### TTL (Time To Live)

El campo **TTL** especifica en **segundos** cuánto tiempo debe almacenarse en caché una respuesta DNS antes de volver a consultarla. Permite reducir el número de consultas repetitivas para dominios populares.

---

## 5. Respuestas a preguntas del módulo

### ¿Qué es DNS?
| Pregunta | Respuesta |
|----------|-----------|
| ¿Qué significa DNS? | Domain Name System |

### Jerarquía de Dominios
| Pregunta | Respuesta |
|----------|-----------|
| Longitud máxima de un subdomain | 63 caracteres |
| ¿Qué carácter NO puede usarse en un subdomain? (`3 b _ -`) | `_` (guión bajo) |
| Longitud máxima de un nombre de dominio completo | 253 caracteres |
| ¿Qué tipo de TLD es `.co.uk`? | ccTLD |

### Tipos de Registros
| Pregunta | Respuesta |
|----------|-----------|
| ¿Qué tipo de registro indica dónde enviar correo? | MX Record |
| ¿Qué tipo de registro maneja direcciones IPv6? | AAAA Record |

### Haciendo una Consulta DNS
| Pregunta | Respuesta |
|----------|-----------|
| ¿Qué campo especifica cuánto tiempo debe guardarse en caché un registro? | TTL |
| ¿Qué tipo de servidor DNS suele proveer tu ISP? | Recursive DNS Server |
| ¿Qué tipo de servidor almacena todos los registros de un dominio? | Authoritative DNS Server |

---

## 6. Análisis y conceptos clave para ciberseguridad

1. **DNS Spoofing / Cache Poisoning:** Un atacante inyecta registros DNS falsos en la caché de un Recursive DNS Server, redirigiendo a los usuarios a sitios maliciosos sin que lo noten. Mitigación: DNSSEC (DNS Security Extensions).

2. **DNS Exfiltration:** Los atacantes pueden usar consultas DNS para exfiltrar datos codificados en los subdominios (ej: `datos_robados.attacker.com`). Al ser tráfico DNS, frecuentemente pasa desapercibido por firewalls que no inspeccionan DNS.

3. **Subdomain Takeover:** Si una empresa registra un CNAME hacia un servicio de terceros (ej: Heroku, GitHub Pages) y luego abandona ese servicio sin eliminar el registro DNS, un atacante puede reclamar ese servicio y controlar el subdominio.

4. **Registros TXT y reconocimiento:** Durante el reconocimiento (OSINT), los registros TXT de un dominio pueden revelar servicios usados por la organización (Google Workspace, Microsoft 365, Mailchimp, etc.), reduciendo el tiempo de enumeración.

5. **TTL bajo como indicador de actividad sospechosa:** Un TTL muy bajo (ej: 60 segundos) puede indicar **Fast Flux DNS**, una técnica usada por botnets para cambiar rápidamente las IPs asociadas a su infraestructura de C2 y evadir bloqueos.

6. **MX Records en ataques de phishing:** Configurar registros MX falsos o SPF/DMARC incorrectos permite a atacantes suplantar dominios legítimos en campañas de phishing. Verificar registros TXT SPF y DMARC es parte del hardening básico de correo.

---
