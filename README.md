# apache

Reemplace `$ALUMNO` por el nombre de su nombre de usuario en www.tecnologoinformatico.com

EJ: `dmascheroni`

1. Cree el directorio ~/repositorios y dentro clone el
repositorio: `https://github.com/TecnologoInformatico/AdmInf-web.git`
2. Actualice el repositorio de la lista de paquetes.
    `apt update`
3. Instalar el servidor Apache mediante apt.
4. Cree el directorio /var/www/$ALUMNO
5. Asigne como propietario del directorio su usuario.
6. Configure un nuevo Virtual host. (copiando el archivo de configuración por defecto)
  6.1. ServerName $ALUMNO.tecnologoinformatico.com
  6.2. Correo de contacto con el administrador.
  6.3. El root de la aplicación. (/var/www/$ALUMNO)
7. Modifique el archivo /etc/hosts de modo que el ServerName coincida con este equipo `127.0.0.1`.
8. Reinicie el servidor apache para que los cambios tengan efecto.
9. Copie el contenido del directorio ~/repositorios/AdmInf-web a /var/www/$ALUMNO, de tal modo que el contenido del repositorio antes clonado se encuentre en el root de la aplicación.
10. Verifique que el servidor funcione correctamente.
11. Ingrese la IP del servidor y el servername a continuación:

```json
{
    "serverName": "",
    "ip": ""
}
```


## Resolucion

1. Clonamos el repo en la nueva carepta creada
```
mkdir ~/repositorios
```
```
https://github.com/TecnologoInformatico/AdmInf-web.git
```
2.
``` bash
sudo apt update
```
```
sudo apt install apache2
```
3.
```
sudo mkdir -p /var/www/molivera
```
4. Ejecutamos el suigente comando para cambiar los permisos del usuario logueado actualmente sobre el directorio recien creado , para ser el owner
Si no sabemos que usuarios estamos logueados podemos ejecutar el comando `whoami`


5.
```
sudo chown ubuntu /var/www/molivera/
```
6.
Primeros nos movemos a la carpeta `/etc/apache2$ cd sites-available/`
Ejecutamos el suigente comando para ver la info por defecto
```
sudo cp 000-default.conf my_site.conf
```
Ejecutamos el comando nano con el archiivo recien creado y pegamos lo siguiente:
```
sudo nano my_site.conf
```
``` conf
<VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        ServerName molivera.tecnologoinformatico.com

        ServerAdmin maximiliano.olivera@dualbootpartners.com
        DocumentRoot /var/www/molivera

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet

```

7.
```
sudo nano /etc/hosts
```
Y agregaremos la ip localhost: 127.0.0.1 con el dominio agregado en el archivo anterior
Luego ejecutaremos 
```
sudo a2ensite my_site.conf
```
8.
Reiniciamos el servidor
```
sudo systemctl reload apache2
```
9. Ejecutamos el siguiente comando para copiar el contenido a la carpeta root de nuestro virtual host
```
sudo cp -a ~/repositorios/AdmInf-web/. /var/www/molivera
```
10. Para probar podemos reiniciar el servidor de apache 
```
sudo systemctl reload apache2
```
Y ejecutar el suguiente comando curl
```
curl molivera.tecnologoinformatico.com
```
11. 
``` json
{
    "serverName": "molivera.tecnologoinformatico.com",
    "ip": "140.238.187.196"
}
```