# 1. Windows: *Server*
- Configurar dos máquinas Windows (7,8,10)

![](./images/captura1.png)  

- Descargar TightVNC.

![](./images/captura5.png)  

- E instalar el *Server* 

![](./images/captura9.png)

- Revisar que la configuración del cortafuegos del servidor VNC Windows para permitir VNC.

![](./images/captura2.png)  

## 1.2 Windows: *Cliente*

- En el cliente instalar `TightVNC -> Custom -> **Viewer**`.

![](./images/captura8.png)  

## 2. Comprobaciones finales

- Conectar desde Windows *Server* hacia el Windows *Cliente*.

- Introducir la IP del cliente

![](./images/captura5.png)  

- Y nos saldra el escritorio del cliente

![](./images/captura4.png)

- Ir al servidor VNC y usar el comando netstat -n para ver las conexiones VNC con el cliente.

![](./images/captura7.png)