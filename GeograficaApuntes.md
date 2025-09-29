# Apuntes Sistemas de Informacion Geograficos

Por el momento super desordenado, refinar para estudiar de mejor manera

## Por que usar un sistema de info geografico?
La informacion que usamos dia a dia consta 70% de informacion geografica, un SIG es capaz de proveer respuestas sobre posicion, topologia, atributos sobre alguna consulta en especifica    

## Historia y problemas

Los fenicios hicieron los primeros vestigios de la cartografia, los griegos dieron saltos considerables a la forma de usarla. Manualmente surgieron los problemas de confiabilidad, perdida de mapas, lentitud en recuperacion de datos, dificil adapatacion (debido a escalas).
En los 60s con el computador a su lado tambien surgió la cartografia automatizada, en 1969 Lan Marchang publico un gran avance como el libro de Design with Nature lanza una técnica SCA (Análisis de Aptitud y capacidad de la tierra)

- En harvard 1964 se realiza los primeros prototipos con mapas simples con puntos y lineas
- Canada desarrolla CGIS por Roger Tomlinson: padre del sig. Formalmente el primer SIG con uso de DBMS

## Definicion de un sig

Es una coleccion organizada de Hardware, software y datos geograficos y personal asignado para la captura, almacenaje, actualizacion, manipuleo, analisis y despliegue de todas las formas de informacion referenciada geográficamente

## Partes de un SIG
1. Datos. Los cuales pueden ser mapas digitales o fisicos, constituyentes de puntos, lineas, areas y complejos
2. SIG. La pieza de software, constituida de un RDBMS y un analisador de los datos
3. Informacion. Datos de salida como esquemas, tablas, listas, mapas nuevos

## Operaciones Espaciales
Varios programas que pueden manejar conjuntos de datos, como ser coordenadas, no son considerados sig porque no pueden responder consultas espaciales. 

- Consulta espacial. Que se encuentra en esta coord(x,y), que pozos petroleros hay en el norte de SCZ
- Consulta no espacial. Cuantos pozos hay en bolivia, numero promedio de gente usa SIG en SCZ

## Union de datos - Emparejado borroso
Como se relacionan diferentes conjuntos de datos, un dbms usa **emparejado exacto**
Por jerarquia de datos es **Emparejamiento Jerarquico**

Un sig usa **Emparejado Borroso**, que relaciona los datos con referencias geograficas. Ej coord(x,y) en varias capas de mapas

------------
# Apuntes de clase - Sistemas de Informacion Geográficos
**Clase 17/09/2025**
## Modelo de datos vector 

representa caracteristicas geograficas similares a los matas.
Usa: puntos, lineas, areas.
Cada posicion es registrada como una coord
usando puntos, lineas, areas


### punto
es solo un punto en las coords x,y

### Lineas 
es un conjunto de coords totalmente diferentes

### Poligono
Secuencia de coords donde la 1er y ultima coord se repiten

## Estructura de datos Arco-Nodo

no permite que existe la misma linea entre poligonos colisionando (ej: 2 cuadrados lado a lado)

3 conceptos
- conectividad. 
- contiguidad
- awa


## Modelo de raster

pixeles jijua


Vectorial es mejor para exactitud frfr