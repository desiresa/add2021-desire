# Vagran con VirtualBox

## (3.3) Comprobar proyecto 1
Vamos a crear una MV nueva y la vamos a iniciar usando Vagrant:
- Debemos estar dentro de `vagrant18-celtics`.
- `vagrant up`, para iniciar una nueva instancia de la máquina.

![](./images/1.png)

- `vagrant ssh`: Conectar/entrar en nuestra máquina virtual usando SSH.

![](./images/2.png)

![](./images/3.png)

## (5.2) Comprobar proyecto 2
Para confirmar que hay un servicio a la escucha en 4567, desde la máquina real podemos ejecutar los siguientes comandos:

- En el HOST-CON-VAGRANT. Comprobaremos que el puerto 4567 está a la escucha.
  - `vagrant port` para ver la redirección de puertos de la máquina Vagrant.

![](./images/20.png)


  - En HOST-CON-VAGRANT, abrimos el navegador web con el URL `http://127.0.0.1:4567`.

![](./images/6.png)

## (6.1) Suministro Shell Script
Ahora vamos a suministrar a la MV un pequeño script para instalar Apache.
- Crear directorio `vagrant18-lakers` para nuestro proyecto.

- Entrar en dicha carpeta.

- Crear fichero `html/index.html` con el siguiente contenido:

![](./images/7.png)

- Crear el script `install_apache.sh`, dentro del proyecto con el siguiente contenido:

![](./images/8.png)

Iniciar en el fichero de configuración `Vagrantfile` lo siguiente:

> config.vm.hostname = "desire18-lakers"
  config.vm-provision :shell, :path => "install_apache.sh"
  config.vm.synced_folder "html", "/var/www/html"

![](./images/9.png)

- `vagrant up`, para crear la MV.


- Para verificar que efectivamente el servidor Apache ha sido instalado e iniciado, abrimos navegador en la máquina real con URL `http://127.0.0.1:4567`.

![](./images/10.png)


## (6.2) Suministro Puppet

Se pide hacer lo siguiente.

- Crear directorio `vagrant18-raptors` como nuevo proyecto Vagrant.
- Modificar el archivo `Vagrantfile` de la siguiente forma:

![](./images/11.png)

- Ahora hay que crear el fichero `manifests/desire18.pp`, con las órdenes/instrucciones Puppet para instalar un programa determinado.

![](./images/12.png)


- Para que se apliquen los cambios de configuración, hacemos `vagrant relodad o restart`.

![](./images/13.png)



## (7.2) Crear Box Vagrant

Una vez hemos preparado la máquina virtual ya podemos crear el box.

- Vamos a crear una nueva carpeta `vagrant18-bulls`, para este nuevo proyecto vagrant.

- `VBoxManage list vms`, comando de VirtualBox que muestra los nombres de nuestras MVs. Elegir una de las máquinas (VMNAME).

![](./images/14.png)

- Nos aseguramos que la MV de VirtualBox VMNAME está apagada.


- `vagrant package --base VMNAME desire18.box`, para crear nuestra propia caja.

![](./images/15.png)

- Comprobamos que se ha creado el fichero `package.box` en el directorio donde hemos ejecutado el comando.

![](./images/21.png)

- `vagrant box add desire/bull package.box`, añadimos la nueva caja creada por nosotros, al repositorio local de cajas vagrant de nuestra máquina.

![](./images/16.png)

- `vagrant box list`, consultar ahora la lista de cajas Vagrant disponibles.

![](./images/17.png)
