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

255.255.255.1111 1000

Ejercicio 2 - Subnetting

| HOSTS | MASCARA             | D.RED         | D. BROADCAST  | RANGO                         |
| ----- | ------------------- | ------------- | ------------- | ----------------------------- |
| 20    | /27 255.255.255.224 | 192.168.1.0   | 192.168.1.31  | 192.168.1.1  - 192.168.1.30   |
| 20    | /27 255.255.255.224 | 192.168.1.32  | 192.168.1.63  | 192.168.1.33 - 192.168.1.64   |
| 20    | /27 255.255.255.224 | 192.168.1.64  | 192.168.1.95  | 192.168.1.65 - 192.168.1.94   |
| 20    | /27 255.255.255.224 | 192.168.1.96  | 192.168.1.127 | 192.168.1.97 - 192.168.1.126  |
| 4     | /29 255.255.254.248 | 192.168.1.128 | 192.168.1.135 | 192.168.1.129 - 192.168.1.134 |
| 4     | /29 255.255.254.248 | 192.168.1.136 | 192.168.1.143 | 192.168.1.137 - 192.168.1.142 |
| 4     | /29 255.255.254.248 | 192.168.1.144 | 192.168.1.151 | 192.168.1.145 - 192.168.1.150 |
| 4     | /29 255.255.254.248 | 192.168.1.152 | 192.168.1.159 | 192.168.1.153 - 192.168.1.158 |


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
5. En configuracion global, con enrutamiento estatico, declarar la red LAN a conectar a través del router vecino (dueño del otro LAN)

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


| HOSTS | MASCARA | D.RED | D. BROADCAST | RANGO |
| ----- | ------- | ----- | ------------ | ----- |
| 89    |         |       |              |       |
| 23    |         |       |              |       |
| 9     |         |       |              |       |
| 2     |         |       |              |       |
| 2     |         |       |              |       |


## Clase 12/09/2025
### Configuracion de credenciales de seguridad en el router

**El Ing mando estas directivas para una topologia de solo un router: **

CONFIGURACOINES BASICAS DE UN ROUTERS

NOMBRE DEL DISPOSITIVO
Router>enable
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#hostname R01
R01(config)#

GRABAR LAS CONFIGURACIONES
R01#copy running-config startup-config 
Destination filename [startup-config]? 
Building configuration...
[OK]

R01#write
Building configuration...
[OK]

R01#w
Building configuration...
[OK]

CONTRASEÑA PARA LA CONSOLA
R01(config)#line console 0
R01(config-line)#password ROBERTOCONSOLA
R01(config-line)#login

CONTRASEÑA PARA EL MODO PRIVILEGIADO
R01(config)#enable secret ROBERTOENABLE

DESACTIVA LA BUSQUEDA DE DNS
R01(config)#no ip domain-lookup

MENSAJE DE BIENVENIDA 
R01(config)#banner motd "INGRESO SOLO A PERSONAL AUTORIZADO"

ENCRIPTAR TODAS LAS CONTRASEÑAS
R01(config)#service password-encryption


HABILITAR SSH PARA PODER ADMINISTRA EL ROUTER REMOTAMENTE

CREAR UN USUARIO CON PRIVILEGIOS
R01(config)#username roberto privilege 15 secret ROBERTOSSH

HABILITAR EL DOMINIO, por acá se conectará el dispositivo a traves de ssh

```
R01(config)#ip domain-name cisco.com
```

HABILITAR LAS CLAVES CRIPTOGRAFICAS PARA RSA
R01(config)#crypto key generate rsa

CONFIGURAR SSH
R01(config)#ip ssh version 2
R01(config)#ip ssh time-out 120
R01(config)#ip ssh authentication-retries 3

CONFIGURAR LAS TERMINALES VIRTUALES Y HABILITAR SOLO SSH
R01(config)#line vty 0 4
R01(config-line)#login loc 
R01(config-line)#transport input ssh

## Clase 15/09/2025. Teoria

### Clasificacion de protocolos de enrutamiento.

- Protocolos classful.
NO envian la mascara de subred durante las actualizaciones de enrutamiento entre ellos: RIP, IGRP.

- Protocolos classles.
Envia la mascara de subred durante las actualizaciones de enrutamiento.

**Convergencia.**
Se define como el estado en que las tablas de enrutamiento de todos los routers son uniformes, practicamente cuando toda la red es totalmente funcional.

### Metricas de los protocolos de enrutamiento.
Es un valor para medir el desempeño y eficiencia del enrutamiento.

**Metricas.**
- Ancho de banda.
- Costo.
- Retraso.
- Conteo de saltos.
- Carga Confiabilidad.


#### Balanceo de Carga.
Cuando 2 rutas tienen las mismas metricas, se divide el envio de datos para mayor velocidad.

#### Distancia admnistrativa de una ruta.



## Clase 17/09/2025

Otros protocolos y mas teoria

### Redistribucion

Acoplarse a una red antigua implica usar otros protocolos en los que ya esta configurado la red, para ello se usa la redistribución de ru enrutamiento

### Bucles de enrutamiento