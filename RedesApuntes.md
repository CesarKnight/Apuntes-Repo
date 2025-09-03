# SUBNETTING

*Dada la red 172.16.64.0 /18. Encontrar:*

1. 5000 hosts
2. 4000 hosts
3. 2000 hosts
4. 1000 hosts
5. 500 hosts
6. 256 hosts

| HOSTS | MASCARA           | D.RED        | D. BROADCAST   | RANGO                         |
| ----- | ----------------- | ------------ | -------------- | ----------------------------- |
| 5000  | /19 255.255.224.0 | 172.16.64.0  | 172.16.95.255  | 172.16.64.1  - 172.16.95.254  |
| 4000  | /20 255.255.240.0 | 172.16.96.0  | 172.16.111.255 | 172.16.96.1  - 172.16.111.254 |
| 2000  | /21 255.255.248.0 | 172.16.112.0 | 172.16.119.255 | 172.16.112.1 - 172.16.119.254 |
| 1000  | /22 255.255.252.0 | 172.16.120.0 | 172.16.123.255 | 172.16.120.1 - 172.16.123.254 |
| 500   | /23 255.255.254.0 | 172.16.124.0 | 172.16.125.255 | 172.16.124.1 - 172.16.125.254 |
| 256   | /23 255.255.254.0 | 172.16.125.0 | 172.16.126.255 | 172.16.125.1 - 172.16.126.254 |

-----------------


# Primera Topografias en Packet Tracer
##  Clase 5 - 29/08/2025 

### Factos

- Cable Directo: Para conectar dispositivos distintos; router - pc.
- Cable cruzado: para conectar dispositivos del mismo tipo como; router - router, pc - pc, etc.

### Comandos de Router

**Comandos de Config Terminal**

```
enable - entrar a modo priviligeado 
configure terminal - entrar a configuraciones globales
copy running-config startup-config - copiar las configuraciones actuales a las iniciales
write - guardar archivo de configuracion 
interface (nombre interfaz) - entrar a las configuraciones de una interfaz (puerto) 
```
-------------------

## Clase 03/09/2025

### Enrutamiento estatico basico

Para comunicacion fuera de una red, es necesario dar a el uso de router (enrutador), el cual se encarga de mostrar la ruta de viaje hacia otra red. El router necesita de configuraciones para cumplir el objetivo de comunicar 2 redes por lo que se hará una red bastante usando *Enrutamiento estatico*

Estatico es la forma mas basica de enrutamiento siendo que este no cambiará por su cuenta ni detectará las redes automaticamente, se hace manualmente toda la configuracion haciendolo bastante sencillo de realizar 

**Ejemplo**
Topografia:

![alt text](Assets/Redes2/topografiaEstatica.png)

Una vez conectados todos los dispositivos tenemos que primero configurar la red lan (Red Area Local). La parte izquierda seria una y la derecha otra
Trabajaremos en la LAN de la izquierda

**Ingresamos a la CLI del router:**

1. Pasamos a modo de configuracion global con los comandos

```bat
enable
configure terminal
```

2. Ingresamos a la configuracion de la interfaz (puerto) a la que esta conectada el switch, en este caso es la Gigabyte 0/0/1
3. Asignamos un

