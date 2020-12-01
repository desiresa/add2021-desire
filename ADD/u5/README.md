# Cliente para autenticación LDAP

# 1. Preparativos

Comprobamos el acceso al LDAP desde el cliente:
- Ir a MV cliente
- `nmap -Pn 172.19.18.31|grep -P '389|636'`, para comprobar que el servidor LDAP es accesible desde la MV2 Cliente

![]()

- `ldapsearch -H ldap://172.19.18.31:389 -W -D "cn=Directory Manager" -b "dc=ldap18,dc=curso2021" "(uid=*)" | grep dn`, comprobamos que los usuarios del LDAP remoto son visibles en el cliente.

![]()

# 2. Configurar autenticación LDAP

## 2.1 Crear conexión con servidor

Vamos a configurar de la conexión del cliente con el servidor LDAP.

- Ir a la MV cliente.

- No aseguramos de tener bien el nombre del equipo y nombre de dominio (/etc/hostname,/etc/hosts).

- Ir a `Yast -> Cliente LDAP y Kerberos`.

- Configurar como la imagen de ejemplo:

  - BaseDN: `dc=ldap18,dc=curso2021`

  - DN de usuario: `cn=Directory Manager`

  - Contraseña: CLAVE del usuario cn=Directory Manager

  ![]()

- Al final usar la opción de `Probar conexión`.

## 2.2 Comprobar con comandos

- Vamos a la consola con ususario root, y probamos lo siguiente:

![]()








# 3. Crear usuarios y grupos dentro del LDAP

En este punto vamos a escribir información dentro del servidor de directorios LDAP. Este proceso se debe poder realizar tanto desde el Yast del servidor, como desde el Yast del cliente.

- Ir a la MV cliente.
- `Yast -> Usuarios Grupos`.
- Set filter: `LDAP users`
- Bind DN: `cn=Directory Manager, dc=ldap18,dc=curso2021`.
- Crear el grupo villanos (Estos se crearán dentro de la ou=groups).
- Crear los usuarios robot, baron (Estos se crearán dentro de la ou=people).
- Consultar/comprobar el contenido de la base de datos LDAP.
  - `ldapsearch -H ldap://172.19.18.31 -W -D "cn=Directory Manager" -b "dc=ldap18, dc=curso2021" "(uid=server18)"` comando para consultar en a base de datos LDAP la información del usuario con uid concreto.
