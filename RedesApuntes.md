# Apuntes de redes
## SUBNETTING

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


**Primera Topografias en Packet Tracer**
### Clase 5 - 29/08/2025 

**Factos**

- Cable Directo: Para conectar dispositivos distintos; router - pc.
- Cable cruzado: para conectar dispositivos del mismo tipo como; router - router, pc - pc, etc.

## Comandos de Router

**Comandos de Config Terminal**

```
enable - entrar a modo priviligeado 
configure terminal - entrar a configuraciones globales
copy running-config startup-config - copiar las configuraciones actuales a las iniciales
write - guardar archivo de configuracion 
interface (nombre interfaz) - entrar a las configuraciones de una interfaz (puerto) 
```
-------------------
## Enrutamiento estatico
### Clase 03/09/2025

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

### Clase 05/09/2025

Realizamos otro enrutamiento:

## Enrutamiento estatico con 3 Wans
![Topografia con 3 Wans y 3 Lans](Assets/Redes2/topografiaEstatica2.png)


Con la red proveida primero debemos subnettear para encontrar las ips para cada red

**Subnetting**

- RED: 192.168.1.0 /24
- Lan1 89 hosts
- Lan2 23 hosts
- Lan3 9 hosts
- todas las WANs 2 hosts


## Configuracion de credenciales de seguridad en el router
### Clase 12/09/2025

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
```
R01(config)#line console 0
R01(config-line)#password ROBERTOCONSOLA
R01(config-line)#login
```

CONTRASEÑA PARA EL MODO PRIVILEGIADO
```
R01(config)#enable secret ROBERTOENABLE
```

DESACTIVA LA BUSQUEDA DE DNS
```
R01(config)#no ip domain-lookup
```

MENSAJE DE BIENVENIDA 
```
R01(config)#banner motd "INGRESO SOLO A PERSONAL AUTORIZADO"
```

ENCRIPTAR TODAS LAS CONTRASEÑAS
```
R01(config)#service password-encryption
```

HABILITAR SSH PARA PODER ADMINISTRA EL ROUTER REMOTAMENTE
CREAR UN USUARIO CON PRIVILEGIOS
```
R01(config)#username roberto privilege 15 secret ROBERTOSSH
```

HABILITAR EL DOMINIO, por acá se conectará el dispositivo a traves de ssh
```
R01(config)#ip domain-name cisco.com
```

HABILITAR LAS CLAVES CRIPTOGRAFICAS PARA RSA
```
R01(config)#crypto key generate rsa
```

CONFIGURAR SSH
```
R01(config)#ip ssh version 2
R01(config)#ip ssh time-out 120
R01(config)#ip ssh authentication-retries 3
```

CONFIGURAR LAS TERMINALES VIRTUALES Y HABILITAR SOLO SSH
```
R01(config)#lin vty 0 4
R01(config-line)#login loc 
R01(config-line)#transport input ssh
```
## Teoria Otros Protocolos
### Clase 15/09/2025. Teoria

**Clasificacion de protocolos de enrutamiento.**

- Protocolos classful.
NO envian la mascara de subred durante las actualizaciones de enrutamiento entre ellos: RIP, IGRP.

- Protocolos classles.
Envia la mascara de subred durante las actualizaciones de enrutamiento.

**Convergencia.**
Se define como el estado en que las tablas de enrutamiento de todos los routers son uniformes, practicamente cuando toda la red es totalmente funcional.

**Metricas de los protocolos de enrutamiento.**
Es un valor para medir el desempeño y eficiencia del enrutamiento.

**Metricas.**
- Ancho de banda.
- Costo.
- Retraso.
- Conteo de saltos.
- Carga Confiabilidad.


**Balanceo de Carga.**
Cuando 2 rutas tienen las mismas metricas, se divide el envio de datos para mayor velocidad.


### Clase 17/09/2025

Otros protocolos y mas teoria


## RIP
### Clase 26/09/2025

Mas Protocolos

**Ripv1** ya no se usa 
**Ripv2**

maximo soporta 15 saltos

**Topografia de prueba**
![topografiaRIP1](Assets/Redes2/topografiaRIP1.png)

1. Hacemos las configuraciones basicas de ip
2. Una vez hecho entrar a las configuraciones de RIP, habilitar la version 2 y deshabilitar autosummary
```
Router(config)#router rip
Router(config-router)#version 2
Router(config-router)#no auto-summary
```
1. Declaramos las redes conectadas al Router. El protocolo se encarga de enrutar a los hosts 
```
Router(config-router)#network 10.0.0.0
Router(config-router)#network 192.168.1.0
```
1. Realizar lo mismo en el otro router
2. Ya ta o.o


### Clase 29/09/2025

Ya un enrutamiento grande para rip


## EIGRP
### Clase 06/10/2025

1. Hacer las configuraciones basicas de los routers
2. En un router crear el proceso de EIGRP con un numero
```
Router(config-router)#router eigrp 100
```
3. Declaramos las redes conectadas al router, cada red debe de ir acompañado de su wildcard. Siendo el wildcard la inversa de la mascara (ej: mask= 255.255.255.0 wildcard= 0.0.0.255)
```
Router(config-router)# network 192.168.2.0 0.0.0.255
Router(config-router)# network 10.0.12.0 0.0.0.3
Router(config-router)# network 10.0.23.0 0.0.0.3
```
4. Realizar el mismo procedimiento en los demas routers
5. ya ta -.-

## OSPF
### Clase 08/10/2025

**Enrutamiento demostracion**

entramos a las config de OSPF

```
Router(config)#router ospf 1
Router(config-router)#network 10.0.0.0 0.0.0.3 area 0
Router(config-router)#network 192.168.1.0 0.0.0.255 area 0
```


### Clase 10/10/2025
## OSPF multiarea

![topografia multiarea](Assets/Redes2/topografiaMultiarea.png)


1. Hacemos las configs basicas de lan y wan
2. Hacemos el router principal de area 0
```
Router(config)#router ospf 1
Router(config-router)#network 192.168.1.0 0.0.0.255 area 0
Router(config-router)#network 10.0.0.0 0.0.0.3 area 0
Router(config-router)#network 10.0.0.4 0.0.0.3 area 0
```
3. Hacemos el router principal en el area 1
```
Router(config)#router ospf 1
Router(config-router)#network 10.0.0.8 0.0.0.3 area 1
Router(config-router)#network 192.168.3.0 0.0.0.255 area 1
Router(config-router)#network 192.168.2.0 0.0.0.255 area 1
```
4. Configuramos el router que esta entre el area 1 y el 0
```
Router(config)#router ospf 1
Router(config-router)#network 10.0.0.0 0.0.0.3 area 0
Router(config-router)#network 10.0.0.8 0.0.0.3 area 1

00:31:22: %OSPF-5-ADJCHG: Process 1, Nbr 192.168.1.1 on Serial0/1/0 from LOADING to FULL, Loading Done
00:32:05: %OSPF-5-ADJCHG: Process 1, Nbr 192.168.3.1 on Serial0/1/1 from LOADING to FULL, Loading Done
```
Los mensajes de Loading Done nos confirman que ospf encontró las redes publicadas

5. Configuracion del router de area 2
```
Router(config)#router ospf 1
Router(config-router)#network 10.0.0.12 0.0.0.3 area 2
Router(config-router)#network 192.168.4.0 0.0.0.255 area 2
Router(config-router)#network 192.168.5.0 0.0.0.255 area 2
```
6. Configuracion del router entre area 0 y 2
```
Router(config-router)#router ospf 1
Router(config-router)#network 10.0.0.4 0.0.0.3 area 0
Router(config-router)#network 10.0.0.12 0.0.0.3 area 2

00:37:22: %OSPF-5-ADJCHG: Process 1, Nbr 192.168.1.1 on Serial0/1/1 from LOADING to FULL, Loading Done
00:37:49: %OSPF-5-ADJCHG: Process 1, Nbr 192.168.5.1 on Serial0/1/0 from LOADING to FULL, Loading Done

```

## Redistribucion entre Enrutamientos

Cuando existen distintas redes que cada una esta configurada con un diferente protocolo de enrutamiento, pero necesitan comunicarse se usa Redistribución.
Normalmente es un router el encargado de comunicar dos redes y se debe aplicar configuraciones para ambos lados 

**Ej**: A es un red con RIP y B es una red con OSPF. En el router que comparte ambos protocolos, es necesario hacer redistribucion tanto de A -> B como de B -> A, asi asegurando comunicacion

Muchos comandos vienen con valores fijos los cuales son los recomendados para la redistribucion, solo cambiar los valores dentro de los []

**OSPF > EIGRP** 
```
router eigrp [# grupo eigrp]
redistribute ospf [# procedimiento ospf] metric 1500 100 255 1 1500
```
**EIGRP > OSPF**
```
router ospf [# procedimiento ospf]
redistribute eigrp [# grupo eigrp] metric 1000 metric-type 1 subnets
```

**OSPF > RIP**
```
router rip
redistribute ospf [# procedimiento ospf] metric 2
```
**RIP > OSPF**
```
router ospf [# procedimiento ospf]
redistribute rip metric 20 metric-type 1 subnets
```

**RIP > EIGRP**
```
router eigrp [# grupo eigrp]
redistribute rip metric 768 2000 255 1 1500
```
**EIGRP > RIP**
```
router rip
redistribute eigrp [# grupo eigrp] metric 3
```

## DHCP
### Clase 13/10/2025

1. Hacer la configuracion basica
2. Configurar DHCP en un router, este proveera las direcciones ip a la red
```
Router(config)#ip dhcp excluded-address 192.168.1.1
Router(config)#ip dhcp pool LAN1
Router(dhcp-config)#network 192.168.1.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.1.1
Router(dhcp-config)#dns-server 8.8.8.8
Router(dhcp-config)#domain
Router(dhcp-config)#domain-name cisco.com
```
3.  Entramos a las computadoras conectadas a la red y Asignamos a cada una a que pida direccion ip con DHCP
4.  Para llegar a un router dhcp de otro, ingresar a la interfaz por donde llegaria la peticion de solicitud dhcp y redireccionar al router dhcp con:
```
ip helper-address 10.0.0.1
```

## Servidores
#### Clase 15/10/2025

![topologia con servidores dhcp, dns, web](Assets/Redes2/TopologiaServidores.png)

Los servidores deben ser enrutados fijamente para que siempre comunicarse con ellos sin variabilidad
En el enrutamiento para los hosts debemos reservar esas direcciones, en caso de ospf excluyendo el rango necesario

**Servidor DHCP**
1. Primero conectar con el router como gateway
2. Asignar su direccion ip
3. En la pagina de configuraciones seguir con:
   1. En servicios activar dhcp
   2. Agregar el router principal como gateway y el servidor dns
   3. Crear un Pool de direcciones por cada subred necesaria
   4. añadir el pool y guardar las configs


**Servidor DNS**
1. Primero conectar con el router como gateway
2. Asignar su direccion ip
3. En la pagina de configuraciones seguir con:
   1. Activar dns en servicios
   2. Añadir los ips con su respectivo dominio

Todos los dispositivos que quieran usar dns tendran que ser proveidos en su configuracion, puede ser tanto estatico como proveido con DHCP

**WEB**

1. Primero conectar con el router como gateway
2. Asignar su direccion ip
3. En la pagina de configuraciones seguir con:
   1. Encender la funcion HTTPS, HTTP
   2. Configurar a gusto los archivos html




#### Clase 22/10/2025

**PRACTICA**

![practica1](Assets/Redes2/practica1.png)



1. Subnetting

| LAN  | Subred           | Máscara         | Dirección de red | Broadcast     | Rango de hosts                |
| ---- | ---------------- | --------------- | ---------------- | ------------- | ----------------------------- |
| LAN1 | 102.168.1.0/27   | 255.255.255.224 | 102.168.1.0      | 102.168.1.31  | 102.168.1.1 - 102.168.1.30    |
| LAN2 | 102.168.1.32/27  | 255.255.255.224 | 102.168.1.32     | 102.168.1.63  | 102.168.1.33 - 102.168.1.62   |
| LAN3 | 102.168.1.64/27  | 255.255.255.224 | 102.168.1.64     | 102.168.1.95  | 102.168.1.65 - 102.168.1.94   |
| LAN4 | 102.168.1.96/27  | 255.255.255.224 | 102.168.1.96     | 102.168.1.127 | 102.168.1.97 - 102.168.1.126  |
| LAN5 | 102.168.1.128/27 | 255.255.255.224 | 102.168.1.128    | 102.168.1.159 | 102.168.1.129 - 102.168.1.158 |


| WAN  | Subred           | Máscara         | Dirección de red | Broadcast     | Rango de hosts                |
| ---- | ---------------- | --------------- | ---------------- | ------------- | ----------------------------- |
| WAN1 | 102.168.1.160/30 | 255.255.255.252 | 102.168.1.160    | 102.168.1.163 | 102.168.1.161 - 102.168.1.162 |
| WAN2 | 102.168.1.164/30 | 255.255.255.252 | 102.168.1.164    | 102.168.1.167 | 102.168.1.165 - 102.168.1.166 |
| WAN3 | 102.168.1.168/30 | 255.255.255.252 | 102.168.1.168    | 102.168.1.171 | 102.168.1.169 - 102.168.1.170 |
| WAN4 | 102.168.1.172/30 | 255.255.255.252 | 102.168.1.172    | 102.168.1.175 | 102.168.1.173 - 102.168.1.174 |
| WAN5 | 102.168.1.176/30 | 255.255.255.252 | 102.168.1.176    | 102.168.1.179 | 102.168.1.177 - 102.168.1.178 |
| WAN6 | 102.168.1.180/30 | 255.255.255.252 | 102.168.1.180    | 102.168.1.183 | 102.168.1.181 - 102.168.1.182 |
| WAN7 | 102.168.1.184/30 | 255.255.255.252 | 102.168.1.184    | 102.168.1.187 | 102.168.1.185 - 102.168.1.186 |


2. Hacer las configuraciones locales de LAN y WAN
3. OSPF en AREA 0


Para practicar en lugar de hacer area 10 hacer rip
En lugar de area 20 hacer egrp
Area 0 osp
y estatico al server



## ACL

Sirve para bloquear la comunicacion desde ciertos origenes


ACL STANDAR
1. Las ACL estándar son aquellas que van numeradas entre el 1 al 99 y de 1300 a 1999
2. Las ACL estándar solamente pueden bloquear trafico basándose en la dirección ip de origen. Las ACL extendidas miran la ip de origen, la ip de destino, puertos de origen y destino.
3. Por norma general ACL estándar se configuran lo mas cerca posible del destino y las ACL extendidas lo mas cerca del destino.
4. Se puede escribir la palabra "host" para reemplazar una ip con wildcard 0.0.0.0 
5. Se puede escribir la palabra "any" para reemplazar una ip con wildcard 255.255.255.255
6. Todas las ACL llevan una regla implícita al final denominada "deny any" si es estándar y "deny ip any any" si es extendida.
7. Las ACL se ejecutan TOP-DOWN, o sea de arriba hacia abajo; es decir el ROUTER recorre cada una de las sentencias y ejecuta la primera con la que haya coincidencia "match", luego descarta las sucesivas.


```
R3(config)#access-list 1 permit 192.168.1.0 0.0.0.7
R3(config)#access-list 1 deny 192.168.1.0 0.0.0.255
R3(config)#access-list 1 permit any


R3(config)#int g0/0/0
R3(config-if)#ip access-group 1 out

```

### Clase 27/10/2025

**Ejercicio ACL extendido**

**ACL EXTENDIDA**


1. ACL extendida debe estar mas cerca del origen
   
#### Clase 31/10/2025
fucking parcial sorpresa y no fuí


## vLan
### Clase 05/11/2025
![ejemplo vlan](Assets/Redes2/topografiaVlan.png)
Ayuda a hacer separaciones dentro de una propia red


1. Entrar a modo configuracion terminal
2. Darle nombre a la vlans
```
Switch(config)#vlan 10
Switch(config-vlan)#exit
Switch(config)#vlan 20
Switch(config-vlan)#exit
Switch(config)#vlan 30
Switch(config-vlan)#exit
```
1. acceder a las interfaces para asignar el vlan, para seleccionar un rango de interfaces usar
```
Switch(config)#int range fastEthernet 0/1 - fa 0/5
```
2. cambiar el modo del puerto a access
```
Switch(config-if)#switchport mode access 
```
1. Por ultimo designar que acceda a la vlan correspondiente
```
Switch(config-if)#switchport access vlan 10
```

**factos**
- Siempre existe la vlan 1
- Los puertos sin usar deberian asignarse a una dummy vlan


### Clase 12/11/2025
**Para enrutar vlanes que estan en diferentes switches**
Usando un router

1. Segmentamos una interfaz en subinterfaces para cada vLan
```
Router(config)#interface gigabitEthernet 0/0/0.10
Router(config-subif)#encapsulation dot1Q 10
Router(config-subif)#ip add 192.168.10.1 255.255.255.0
Router(config-subif)#ex

Router(config)#interface gigabitEthernet 0/0/0.20
Router(config-subif)#encapsulation dot1Q 20
Router(config-subif)#ip add 192.168.20.1 255.255.255.0
Router(config-subif)#ex

Router(config)#interface gigabitEthernet 0/0/0.30
Router(config-subif)#encapsulation dot1q 30
Router(config-subif)#ip add 192.168.30.1 255.255.255.0
Router(config-subif)#ex
``` 

**Activar la interfaz**

```
Router(config)#int gig0/0/0
Router(config-if)#no sh
```


## Enrutamiento con switch multicapa

![Enrutamiento switch multicapa](Assets/Redes2/enrutamientoSwitchMulticapa.png)
En este caso con VLans


1. Al switch multicapa habilitamos routing con
```
swMulti(config)#ip routing
```
2. Hacemos trunk la interfaces que conecten el switch chikito y el multicapa, en ambos.
aunque cada vez que lo intento me sale que no se puede mover de "auto"
```
swMulti(config)#switchport mode trunk
```
3. Crear las vlans en el switch multicapa, aunque no los usemos directamente.
4. Acceder a cada vlan como si fuera una interfaz y asignar la ip de gateway. Funcionarán como interfaces virtuales
```
swMulti(config)#int vlan 10
swMulti(config-if)#ip address 192.168.10.1 255.255.255.0
swMulti(config-if)#ex
swMulti(config)#int vlan 20
swMulti(config-if)#ip add 192.168.20.1 255.255.255.0
swMulti(config-if)#ex
swMulti(config)#int vlan 30
swMulti(config-if)#ip add 192.168.30.1 255.255.255.0
swMulti(config-if)#ex
```

### Clase 14/11/2025

Para usar DHCP en cada vlan tratar a cada vlan como si fuera una red
```
Router(config)#ip dhcp excluded-address 192.168.40.1
Router(config)#ip dhcp excluded-address 192.168.50.1
Router(config)#ip dhcp excluded-address 192.168.60.1
Router(config)#     ip dhcp pool VLAN1
Router(dhcp-config)#net 192.168.10.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.10.1
Router(dhcp-config)#dns-server 8.8.8.8
Router(dhcp-config)#domain-name cisco.com
Router(dhcp-config)#ex
Router(config)#     ip dhcp pool VLAN5
Router(dhcp-config)#net 192.168.50.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.50.1
Router(dhcp-config)#dns-server 8.8.8.8
Router(dhcp-config)#domain-name cisco.com
Router(dhcp-config)#ex
Router(config)#     ip dhcp pool VLAN6
Router(dhcp-config)#net 192.168.60.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.60.1
Router(dhcp-config)#dns-ser 8.8.8.8
Router(dhcp-config)#domain- cisco.com
Router(dhcp-config)#ex
```


Cuando el switch multicapa debe comunicarse con otro router para el rol de enrutamiento puede ser necesario deshabilitar la funcion de conexion switch en la interfaz, dejando solo la funcion de enrutamiento

```
swMulti(config-if)#no swichtport 
```

### Clase 19/11/2025
Repechaje sorpresa

## Vlan nativa y sw multicapa channel 
### Clase 21/11/2025

en un dispositivo podemos usar multiples conexiones para mayor desempeño con comunicacion paralela, para ello se debe usar el agrupamiento por Channels

## protocolos de channel
lacp es generico
pagp es de cisco

lacp tiene modo Active y Passive. En el enlace entre los 2 dispositivo al menos uno debe ser active
pagp tiene modo auto

1. seleccionar las multiples interfaces para asignar el canal
```
Switch(config)#int range gigabyte 1/0/1-2
```
2. Seleccionamos el protocolo
```
Switch(config-if-range)#channel-protocol lacp
```
3. Asignamos un numero al channel y seleccionamos su modo
```
Switch(config-if-range)#channel-group 1 mode active
```
4. Para buen funcionamiento en routing, una vez creado el channel debemos cambiar su modo a trunk
```
Switch(config)#int port-channel 1
Switch(config-if)#sw mode trunk
```
**Cambiar vlan nativa**

```
sw trunk allowed vlan 40,50,60,99
sw trunk native vlan 99
```

## Switch en medio de vlanes y Router
### Clase 24/11/2025

En caso que exista un switch el cual esta recibiendo mensajes de vlanes, use channels y este debe pasarlo a un router para enrutamiento. Se debe permitir el paso de las vlanes a traves del channel con


Para la navegacion de vlans por cada channel
para cada channel

**NOTA**
Usar por donde sea que entre un vlan!
```
Switch(config-if)#sw trunk allowed vlan 10,20
```


## DHCP POOLS RAPIDO
Probablemente estas sean los pools mas comunes, al pegar multiples comandos en packet se ejecutan, asi que esto deberia ayudar a ser rapido.
```
ip dhcp excluded-address 10.5.3.1
ip dhcp pool VLAN40
net 10.5.3.0 255.255.255.128
default-router 10.5.3.1
dns-server 8.8.8.8
domain-name cisco.com
ex
```
```
ip dhcp pool VLAN1
net 192.168.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 8.8.8.8
domain-name cisco.com
ex
```
```
ip dhcp pool VLAN2
net 192.168.20.0 255.255.255.0
default-router 192.168.20.1
dns-server 8.8.8.8
domain-name cisco.com
ex
```
```
ip dhcp pool VLAN3
net 192.168.30.0 255.255.255.0
default-router 192.168.30.1
dns-server 8.8.8.8
domain-name cisco.com
ex
```
```
ip dhcp pool VLAN4
net 192.168.40.0 255.255.255.0
default-router 192.168.40.1
dns-server 8.8.8.8
domain-name cisco.com
ex
```


## GATEWAY VIRTUAL
### Clase 28/11/2025

![topologia gateway virtual](Assets/Redes2/topologiaGateway.png)

Gateway virtual es una manera de configurar multiples routers gateway, para tener salvaguarda en caso que uno este inactivo 


1. Entrar a la interfaz del router donde se recibiria comunicacion de la red (ej gig0/0/0)
2. Asignar el grupo de gateway virtual, junto con declaracion de ip con standby
3. Asignar prioridad de este router
4. Preparar el gateway con preemp (creo)
```
Router(config-if)#standby 1 ip 192.168.10.100
Router(config-if)#standby 1 priority 100
```
5. En el router que se considere como principal usar
```
Router(config-if)#standby 1 preempt
```

## GATEWAYS VIRTUALES EN SWITCHES MULTICAPA
### Clase 01/12/2025

Super topologia con gateways virtuales y switches multicapa

![topo gateways y multicapas](Assets/Redes2/topologiaGatewaysMulticapa.png)

En este caso las direcciones "reales" serian las que asignamos a las interfaces de las vlanes.
Mientras que, en cada interfaz de vlan tambien tenemos que crear un gateway virtual.

No olvidar usar los switches multicapa como routers con el comando
```
ip routing
```
y en caso de ser puertos donde se enrutará con direcciones ip fijas, desactivar la funcionalidad de switch (esto hace que funcione como puerto de un router)
```
no switchport
```
por ultimo enrutar todos los routers incluyendo los vlanes