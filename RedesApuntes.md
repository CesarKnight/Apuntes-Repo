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

![Topografia estatica de 2 lans](Assets/Redes2/topografiaEstatica.png)

Una vez conectados todos los dispositivos debemos primeramente configurar la red lan (Red Area Local). La parte izquierda seria una y la derecha otra
Trabajaremos en la LAN de la izquierda

**Ingresamos a la CLI del router:**

1. Pasamos a modo de configuracion global con los comandos

```
enable
configure terminal
```

2. Ingresamos a la configuracion de la interfaz (puerto) a la que esta conectada el switch, en este caso es la Gigabyte 0/0/1

```
interface gigabyte 0/0/1
```

3. Definimos la direccion de la red asignando una ip al router. Usando la red proveida y su Máscara
Ej. Si la direccion de la red debe ser 192.168.1.0 asignamos la ip 192.168.1.1 al router. Tomar en cuenta que estamos asignando la direccion a la interfaz (direccion del router dentro esta lan)

```
ip address 192.168.1.1 255.255.255.0
```

4. Configurar cada PC conectada a la LAN a través del switch de la siguiente manera:
   1. Ingresar a la PC
   2. Entrar a Desktop
   3. Entrar a configuracion de IP
   4. Asignar direccion IP
   5. Asignar Mascara de Subred
   6. En Gateway poner la direccion del router en la LAN
5. Realizar los pasos anteriores en las otras LANs
   
**Conexion entre redes (WAN)**
En esta etapa es donde usamos enrutamiento estatico para intercomunicar ambas redes. Esta comunicacion será otra red en totalidad a considerada como WAN
**Ingresamos al CLI de un router:**

1. Ingresamos a Configuracion global
2. Ingresamos a la interfaz de conexion con otro router. En este caso gigabyte 0/0/0

```
interface gigabyte 0/0/0
```

3. Asignamos la direccion del router en la WAN. Si la red wan debe tener la direccion 10.0.0.0 usar 10.0.0.1, ademas de usar la mascara necesaria

```
ip address 10.0.0.1 255.255.255.252
```

4. Realizar los pasos anteriores en el router vecino a conectar
5. En configuracion global asignar, con enrutamiento estatico, declarar la red LAN a conectar a través del router vecino (dueño del otro LAN)

```
ip route 192.168.2.0 255.255.255.0 10.0.0.2
```

6. Realizar los pasos en los routers necesarios

## Clase 05/09/2025

Realizamos otro enrutamiento:

### Enrutamiento estatico con 3 Wans
![Topografia con 3 Wans y 3 Lans](Assets/Redes2/topografiaEstatica2.png)


Con la red proveida primero debemos subnettear para encontrar las ips para cada red

**Subnetting**

- RED: 192.168.1.0 /24
- Lan1 89 hosts
- Lan2 23 hosts
- Lan3 9 hosts
- todas las WANs 2 hosts


| HOSTS | MASCARA           | D.RED        | D. BROADCAST   | RANGO                         |
| ----- | ----------------- | ------------ | -------------- | ----------------------------- |
| 89    | /19 255.255.224.0 | 172.16.64.0  | 172.16.95.255  | 172.16.64.1  - 172.16.95.254  |
| 23    | /20 255.255.240.0 | 172.16.96.0  | 172.16.111.255 | 172.16.96.1  - 172.16.111.254 |
| 9     | /21 255.255.248.0 | 172.16.112.0 | 172.16.119.255 | 172.16.112.1 - 172.16.119.254 |
| 2     | /22 255.255.252.0 | 172.16.120.0 | 172.16.123.255 | 172.16.120.1 - 172.16.123.254 |
| 2     | /23 255.255.254.0 | 172.16.124.0 | 172.16.125.255 | 172.16.124.1 - 172.16.125.254 |