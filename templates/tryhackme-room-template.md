# Fundamentos de Redes — Resumen y Análisis

> **Módulo:** Pre-Security / Network Fundamentals  
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
