### Prerrequisitos:

-   [Configurar NAT](https://docs.google.com/document/u/0/d/17EoapDIAgUI1Uhq5MuZwZ9kmRsT12SVEy31VmuQj2Gw/edit)
    
-   [Configurar tarjeta de red](https://docs.google.com/document/u/0/d/17EoapDIAgUI1Uhq5MuZwZ9kmRsT12SVEy31VmuQj2Gw/edit)
    

# Instalación del servidor

```sudo apt install proftpd -y```

Una vez instalado ya podríamos conectarnos por FTP con un cliente como por ejemplo FileZilla a nuestro servidor con una cuenta de usuario que exista en el servidor. Cabe destacar que no podremos subir archivos en cualquier directorio.

![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fub0q4WV9Z6MJbyvmj80I%2Fuploads%2FzdSzSVjyvEsidgm5FzI5%2F0?alt=media)

Write a caption

## Cambiar nombre al servidor

En la línea que pone `ServerName “Debian”` podemos cambiar el nombre por el que queramos, en nuestro caso hemos puesto **ivegamerayo** por ser el nombre corporativo.

# Configuración básica

## Encerrar a un usuario

Con las siguientes líneas encerramos a un usuario y pedimos los usuarios virtuales que se encuentran en el archivo ftpd.passwd que crearemos más [adelante](/s/ub0q4WV9Z6MJbyvmj80I/c/PhnlU3xYCxUrdtFWNgUU/#_s5w75hxrozk7).

`DefaultRoot ~`

`RequireValidShell off`

`AuthUserFile /etc/proftpd/ftpd.passwd`

El archivo final sería así

Write a caption

## Creación usuarios

## Crear un usuario

En nuestro caso vamos a crear un usuario llamado **test** el cual tendrá su home en /var/www/html/todo-empresaivm04, para ello utilizaremos el siguiente comando:

`sudo ftpasswd --passwd --file=/etc/proftpd/ftpd.passwd --name=test --uid=60 --gid=60 --home=/var/www/html/todo-empresa-ivm04 --shell=/bin/false`

-   **--file=** ruta_archivo
    
-   **--name=** nombre_usuario
    
-   **--uid=** id_usuario
    
-   **--gid=** grupo
    
-   **--home=** ruta_home_usuario
    
-   **--shell**=shell_usuario
    

## Crear un grupo

No es totalmente necesario, además en esta documentación no explicamos como usarlo.

`sudo ftpasswd --group --name=nogroup --file=/etc/proftpd/ftpd.group --gid=60 --member test`

## Comprobar la configuración

`sudo proftpd -t`

## Reiniciar y comprobar los cambios

`sudo service proftpd restart`

`sudo service proftpd status`

## Cambiar la contraseña

`sudo ftpasswd --passwd --file=/etc/proftpd/ftpd.passwd --name=test --change-password`

## Eliminar usuario

`sudo ftpasswd --passwd --file=/etc/proftpd/ftpd.passwd --name=test --delete-user`

# Crear directorio para usuario
