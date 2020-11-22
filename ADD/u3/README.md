# Servidor de Impresión GNU/Linux (CUPS)
## 2. Comprobar que el Servicio está en ejecución

- Instalar el sistema de impresión de CUPS para GNU/Linux.

![](./images/servidor/1.png)

- `Systemctl status ...`, verificar que el servicio está en ejecución.

![](./images/servidor/2.png)

- Configurar CUPS `/etc/cups/cupsd.conf`:

  - `Listen *:631`

  - `<Location> Allow @LOCAL`

![](./images/servidor/4-2.png)

![](./images/servidor/4.png)

- `systemctl restart ...`

- A continuación, conectar a la inerfaz web de CUPS `localhost:631`

![](./images/servidor/3.png)

- Acceder a la seccion de Administración con el usuario/clave de root. Desde ahí acceder a la seccion `Ver archivo de registro de accesos.`

![](./images/servidor/8.png)

# 3. Comprobar que se imprime de forma local

Ahora vamos a usar una impresora de forma local en el servidor de impresión.

- Instalar el paquete `cups-pdf` que nos permite hacer uso de una impresora virtual PDF local. Usaremos esta impresora virtual para las pruebas en caso de no disponer de una impresora real => `apt-get install cups-pdf`.

![](./images/servidor/9.png)

- Crear un archivo TXT o ODT con algún contenido.

- Imprimir el documento en la impresora local.

![](./images/servidor/16.png)

- Comprobar el resultado. Los trabajos de impresión de la impresora virtual PDF se guardan en alguno de estos directorios.

  >/home/desire/PDF
  >/var/spool/cups-pdf/server18g


# 4. Comprobar que se imprime de forma remota

En el Servidor
- Habilitar la impresora como recurso de red compartido.

![](./images/servidor/15.png)

En el cliente

- Agregar impresora de red.

![](./images/cliente/1.png)

- Crear un archivo TXT u ODT con algún contenido.

- Imprimir el documento en la impresora remota.

![](./images/cliente/3.png)

- Comprobar desde el servidor que se ha realizado la impresión remota.

![](./images/servidor/17.png)
