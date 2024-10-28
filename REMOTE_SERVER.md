## Administración remota de servidores
Repetir la práctica anterior pero con un WS Core.
Realizar manual explicando el trabajo realizado. Debe incluir configuración del entorno virtual, configuraciones de red, configuraciones iniciales WS, y como añadir un TrustedHost al panel de administración del servidor.

### Maquinas Virtuales
Necesitamos 2 maquinas, una tiene que ser `WindowsServerDesktop` y la otra `WindowsServerCore`

### Configuracion Red
Vamos a usar una red de clase `A` con lo siguiente
 - `Srv 1` / `10.10.1.10/24`
 - `Srv 2` / `10.10.1.12/24`
 - `Mascara de red` / `255.255.255.0`
