## Servidor Samba (MV1)

# (1.4) Configurar el servidor Samba

- `cp /etc/samba/smb.conf /etc/samba/smb.conf.bak`, hacer una copia de seguridad del fichero de configuración antes de modificarlo.

![](images/server/samba.png)

# (1.5) Crear los recursos compartidos de red

Vamos a configurar los recursos compartidos de red en el servidor, modificando el fichero de configuración

    [global]
      netbios name = server18g
      workgroup = curso2021
      server string = Servidor de desire18
      security = user
      map to guest = bad user
      guest account = sambaguest

    [public]
      comment = public de desire18
      path = /srv/samba18/public.d
      guest ok = yes
      read only = yes

    [castillo]
      comment = castillo de desire18
      path = /srv/samba18/castillo.d
      read only = no
      valid users = @soldados

    [barco]
      comment = barco de desire18
      path = /srv/samba18/barco.d
      read only = no
      valid users = pirata1, pirata


![](images/server/10.png)


- `testparm`, para verificar la sintaxis del fichero de configuración
- `more /etc/samba/smb.conf`, consultar el contenido del fichero de configuración


![](images/server/11.png)


# (2.1) Cliente Windows GUI

Desde el cliente Windows vamos a acceder a los recursos compartidos del servidor Samba

- Escribimos \\172.19.18.31 y vemos lo siguiente.

- Accedemos al recurso compartido "barco" con el usuario "pirata1"

![](images/windows/2.png)

  - net use para ver las conexiones abiertas

    - net use * /d /y, para borrar todas las conexiones SMB/CIFS que se han realizado.  

![](images/windows/12.png)

- Acceder al recurso compartido con el usuario pirata.
- Ir al servidor Samba.
- Comprobar los resultados

- `smbstatus`, desde el servidor Samba.

![](images/server/windows1.png)

- `lsof-i`, desde el servidor Samba.

![](images/server/windows2.png)

## (2.2) Cliente Windows comandos

- Abrir una shell de windows
- `net use`, para consultar todas las conexiones/recursos conectados.

![](images/windows/33.png)

- Si hubiera alguna conexión abierta la cerramos.
  - `net use * /d /y`, para cerrar las conexiones SMB.
  - `net use`, ahora vemos que no hay conexiones establecidas.

- `net view \\172.19.18.31`, para ver los recursos de esta máquina.

![](images/windows/14.png)

- Montar el recurso barco de forma persistente.

- `net use S: \\IP-SAMBA\barco contraseña /USER:pirata1 /p:yes` crear una conexión con el recurso compartido y lo monta en la unidad S. (con /p:yes hacemos el montaje persistente).

![](images/windows/15.png)

- `net use`, comprobamos.

- Ahora podemos entrar en la unidad S:, y crear carpetas, ficheros, etc.

![](images/windows/17.png)

![](images/windows/20.png)

- `smbstatus`, desde el servidor Samba.

![](images/server/windows3.png)

- `lsof -i`, desde el servidor Samba.

![](images/server/windows4.png)

# 3. Cliente GNU/Linux

## (3.1) Cliente GNU/Linux GUI

Desde el entorno gráfico de client18g, podemos comprobar el acceso a recursos compartidos SMB/CIFS.

- Vamos a una carpeta, y escribimos en la ruta `smb://172.19.18.31`.

![](images/cliente/1.png)

- Probamos a crear carpetas en `barco`.

![](images/cliente/2.png)

- Comprobamos en el servidor Samba:

- `smbstatus`

![](images/server/client1.png)

- `lsof -i`

![](images/server/client2.png)

# 3.2 Cliente GNU/Linux comandos

- Vamos a nuestro cliente Samba de Linux. Desde este equipo accederemos a la carpeta compartida.

- Probar desde el cliente, el comando `smbclient --list 172.19.18.31`.

![](images/cliente/15.png)

- Ahora crearemos en local la carpeta `/mnt/remoto18/castillo`.

- Con el usuario root, usamos el siguiente comando para montar un recurso compartido de Samba Server, como si fuera una carpeta más de nuestro sistema: `mount -t cifs //172.19.18.31/castillo /mnt/remoto18/castillo -o username=soldado1`.

- `df -hT`, para comprobar que el recurso ha sido montado.

![](images/cliente/22.png)

- Y comprobamos desde el Servidor:
  - `sudo smbstatus`.

![](images/server/20.png)

  - `sudo lsof -i`.

![](images/server/2.png)
