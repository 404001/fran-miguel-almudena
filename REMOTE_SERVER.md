## Administración remota de servidores
Repetir la práctica anterior pero con un WS Core.
Realizar manual explicando el trabajo realizado. Debe incluir configuración del entorno virtual, configuraciones de red, configuraciones iniciales WS, y como añadir un TrustedHost al panel de administración del servidor.

### Maquinas Virtuales
Las maquinas tienen que estar en red interna las dos.
Necesitamos 2 maquinas, una tiene que ser `WindowsServerDesktop` y la otra `WindowsServerCore`

En las 2 maquinas tenemos q ejecutar esto para cambiar el nombre de la maquina, cada uno con su nombre correspondiente:
```pws
Rename-Computer -NewName "Srv1" -Restart
```
```pws
Rename-Computer -NewName "Srv2" -Restart
```



## Configuracion Red
Vamos a usar una red de clase `A` con lo siguiente
 - `Srv 1` / `10.10.1.10/24`
 - `Srv 2` / `10.10.1.12/24`
 - `Mascara de red` / `255.255.255.0`

### Configuracion del Server 1
El server 1 es con interfaz grafica, por lo q seria dirigirnos a ajustes adaptador de red, seleccionamos propiedades y `Ipv4`. Ahora pondremos toda la informacion de la red para el server 1.


### Configuracion del Server 2
Este, al ser la version core tendremos que configurarlo por consola. Para ello necesitamos ejecutar los siguientes comandos.

Obtener la ID de los adaptadores de red disponibles:
```pws
Get-NetAdapter
```

Ahora vamos a cambiar la config de la red:

```pws
New-NetIPAddress -InterfaceAlias "nombre_de_adaptador" -IPAddress "10.10.1.12" -PrefixLength 24
```
