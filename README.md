# 🌐 NetPractice - 42 Network Training Tool

NetPractice es un proyecto de la Escuela 42 diseñado para introducir a los estudiantes en los conceptos fundamentales del **networking** (redes de computadoras). A través de una serie de ejercicios prácticos, los estudiantes aprenden a configurar rutas, subredes, direcciones IP, y a entender cómo fluye la información en una red.

---

## 📚 Objetivos del Proyecto

- Comprender el modelo OSI y cómo se relaciona con las redes modernas.
- Aprender a manipular direcciones IP y máscaras de subred.
- Configurar rutas estáticas y examinar el flujo de paquetes.
- Diagnosticar problemas de red mediante pruebas lógicas.
- Desarrollar el pensamiento lógico y sistemático al enfrentar problemas de conectividad.

---
<!--
## 📚 Tabla de Contenidos

1. [Objetivos del Proyecto](#-objetivos-del-proyecto)  
2. [Conceptos Clave](#-conceptos-clave)  
   - [Modelo OSI](#1-modelo-osi-open-systems-interconnection)  
   - [Direccionamiento IP](#2-direccionamiento-ip)  
   - [Subnetting](#3-subnetting-subredes)  
   - [Enrutamiento](#4-enrutamiento-routing)  
   - [Switches y Broadcast](#5-switches-y-broadcast)  
   - [Flow de Paquetes](#6-flow-de-paquetes)  
3. [Guía de Ejecución](#-guía-de-ejecución)  
4. [Comandos y Configuración](#-comandos-y-configuración)  
5. [Tips Comunes](#-tips-comunes)  
6. [Troubleshooting (Solución de Problemas)](#-troubleshooting-solución-de-problemas)  
7. [Recursos Útiles](#-recursos-útiles)  
8. [Créditos](#-créditos)  
9. [Licencia](#-licencia)
-->

## 🧠 Conceptos Clave

### 1. Modelo OSI (Open Systems Interconnection)

El modelo OSI divide la comunicación en redes en 7 capas. En NetPractice trabajamos principalmente con:

- **Capa 3 (Red)**: IP, rutas, encaminamiento.
- **Capa 2 (Enlace)**: direcciones MAC, switches, tramas.
- **Capa 1 (Física)**: cables, hardware de red, conectividad básica.

---

### 2. Direccionamiento IP

- Una **IP** es una dirección lógica usada para identificar dispositivos en una red.
- Formato: `X.X.X.X` (IPv4), donde cada `X` está entre 0-255.
- Ejemplo: `192.168.0.1`

#### Clases de IP

| Clase | Rango Inicial              | Uso común             |
|-------|----------------------------|------------------------|
| A     | 1.0.0.0 – 126.255.255.255  | Grandes organizaciones |
| B     | 128.0.0.0 – 191.255.255.255| Empresas medianas      |
| C     | 192.0.0.0 – 223.255.255.255| Hogares y PYMEs        |

---

### 3. Subnetting (Subredes)

- El **subneteo** permite dividir redes grandes en partes más pequeñas.
- Se define usando una **máscara de subred**: `255.255.255.0`, `/24`, etc.
- Ejemplo:  
  - IP: `192.168.1.0/24`  
  - Rango válido: `192.168.1.1 – 192.168.1.254`  
  - Broadcast: `192.168.1.255`  
  - Gateway típico: `192.168.1.1`

> Las IPs que terminan en `.0` o `.255` **no se asignan** a hosts, ya que son para **red** y **broadcast**.

---

### 4. Enrutamiento (Routing)

- Los **routers** permiten que dispositivos en redes diferentes se comuniquen.
- Si un dispositivo quiere comunicarse fuera de su subred, **envía los datos al router (gateway)**.
- El router usa **rutas estáticas** para saber a dónde enviar el paquete.

#### Configuración típica:

```

IP Address: 192.168.1.2
Mask: 255.255.255.0
Gateway: 192.168.1.1

```

#### En un router:

```

route add 192.168.2.0/24 via 10.0.0.2

```

Esto indica que para llegar a la red `192.168.2.0`, los paquetes deben enviarse a `10.0.0.2`.

---

### 5. Switches y Broadcast

- Los **switches** conectan varios dispositivos en una red local.
- Funcionan en la capa 2, usando direcciones MAC.
- A diferencia de los hubs, los switches **dirigen el tráfico sólo al destino adecuado**.

---

### 6. Flow de Paquetes

Cuando un dispositivo envía un paquete:

1. Verifica si el destino está en la misma red.
2. Si **sí**, lo envía directamente.
3. Si **no**, lo envía al **gateway predeterminado**.
4. El **router** determina por qué interfaz reenviar el paquete.

---

## ⚙️ Comandos y Configuración

### En computadoras

Haz clic en el dispositivo y configura:

- Dirección IP
- Máscara de subred
- Puerta de enlace (gateway)

Ejemplo válido:

```

IP: 192.168.1.2
Mask: 255.255.255.0
Gateway: 192.168.1.1

```

### En routers

En routers debes:

1. Asignar IPs a cada interfaz (debes usar IPs dentro del rango correspondiente).
2. Añadir rutas estáticas para alcanzar redes no conectadas directamente.

Ejemplo:

```

Interface 0: 10.0.0.1/30
Interface 1: 192.168.1.1/24

Static Route:
192.168.2.0/24 via 10.0.0.2

```

---

## 🧪 Tips Comunes

✅ Usa rangos de IP coherentes para cada subred.  
✅ Siempre configura el **gateway correcto**.  
✅ En routers, asegúrate de que ambas interfaces tengan IP.  
✅ Revisa las **máscaras**. Un error de /24 por /25 puede romper la red.  
✅ Usa herramientas visuales de NetPractice para verificar el flujo.

---

## 🛠️ Troubleshooting (Solución de Problemas)

| Problema                         | Causa común                          | Solución                          |
|----------------------------------|--------------------------------------|-----------------------------------|
| No hay conexión entre hosts      | Gateway incorrecto                   | Verifica puerta de enlace         |
| Router no enruta paquetes        | Falta de rutas estáticas             | Añadir rutas con destino y next-hop |
| Switch no reenvía paquetes       | Cable mal conectado o sin IP         | Revisa conexiones y configuraciones |
| Dispositivo dice "not reachable" | IP fuera del rango de subred         | Verifica IP y máscara             |

---

## 📎 Recursos Útiles

- [Cisco Subnetting Tutorial](https://www.cisco.com/c/en/us/support/docs/ip/routing-information-protocol-rip/13788-3.html)
- [Subnetting Practice Tool](https://subnettingpractice.com/)
- [Networking Basics - GeeksForGeeks](https://www.geeksforgeeks.org/basics-computer-networking/)
- [Subnetting & LVMs Calculator](https://arcadio.gq/index.html)

---

<br/>

<div align="center">
  <img src="https://avatars.githubusercontent.com/u/102600920?v=4" alt="Avatar" width="200"/>
  <br/><br/>
  <a href="https://github.com/jfercode">Javier Fernández Correa</a>
</div>

<br/>

<div align="center">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTVInHuUPtp3uiEuvF0aYAkFBUzpnr65b2CDA&s" alt="42 Logo"/>
</div>
