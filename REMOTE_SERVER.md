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

<br>

## Configuracion Red
Vamos a usar una red de clase `A` con lo siguiente
 - `Srv1` / `10.10.1.10/24`
 - `Srv2` / `10.10.1.20/24`
 - `Mascara de red` / `255.255.255.0`

<br>

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
New-NetIPAddress -InterfaceAlias "nombre_de_adaptador" -IPAddress "10.10.1.20" -PrefixLength 24
Set-DnsClientServerAddress -InterfaceAlias "nombre_de_adaptador" -ServerAddresses ("8.8.8.8","8.8.4.4")
```


<br>

## Habilitar el Remote Desktop
En las dos maquinas nos dirigimos a la powershell y pondremos el siguiente comando:

```pws
sconfig
```

Nos saldra un meno y tendremos q poner `4 + enter` y despues `1 + enter` para habilitar el remote desktop.

Ahora poner el ping tendremos q poner lo mismo pero en vez de `1 + enter` es `3 + enter`

## Configuracion en el servidor remoto
Una vez habilitado el remote desktop en los 2 equipos, tendremos q instalar en el servidor remoto `Srv2` lo siguiente:

```pws
Enable-PSRemoting -Force
winrm quickconfig
```

### 1. Configurar el Servidor Local para Confiar en el Servidor Remoto (Trusted Host)
En el servidor local (no en el Core), añade la IP del servidor Core como Trusted Host para permitir la administración remota. En el servidor local, ejecuta el siguiente comando en PowerShell:

```pws
Set-Item WSMan:\localhost\Client\TrustedHosts -Value "10.10.1.20"
```

### 2. Configuración de Credenciales en el Servidor Local
Para almacenar las credenciales de acceso al servidor Core, ejecuta el siguiente comando en el servidor local (no en el Core):

```pws
cmdkey /add:10.10.1.20 /user:vboxuser /pass:changeme
```
