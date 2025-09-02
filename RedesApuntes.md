# **SUBNETTING**

*Dada la red 172.16.64.0 /18. Encontrar:*

1. 5000 hosts
2. 4000 hosts
3. 2000 hosts
4. 1000 hosts
5. 500 hosts
6. 256 hosts

| HOSTS | MASCARA           | D.RED        | D. BROADCAST   | RANGO                          |
| ----- | ----------------- | ------------ | -------------- | ------------------------------ |
| 5000  | /19 255.255.224.0 | 172.16.64.0  | 172.16.95.255  | 172.16.64.1 - 172.16.95.254    |
| 4000  | /20 255.255.240.0 | 172.16.96.0  | 172.16.111.255 | 172.16.96.1 - 172.16.111.254   |
| 2000  | /21 255.255.248.0 | 172.16.112.0 | 172.16.119.255 | 172.16.112.1 - 172.16.119.254  |
| 1000  | /22 255.255.252.0 | 172.16.120.0 | 172.16.123.255 | 172.16.120.1    172.16.123.254 |
| 500   | /23 255.255.254.0 | 172.16.124.0 | 172.16.125.255 | 172.16.124.1    172.16.125.254 |
| 256   | /23 255.255.254.0 | 172.16.125.0 | 172.16.126.255 | 172.16.125.1    172.16.126.254 |

# Primeras weas en Packet Tracer

##  Clase 5 - 29/08/2025 
- [x] asistí

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
