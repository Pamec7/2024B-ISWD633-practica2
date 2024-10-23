# Variables de Entorno
### ¿Qué son las variables de entorno
# COMPLETAR
<pre>
  Las variables de entorno son valores que configuran cómo funcionan el sistema y las aplicaciones, como rutas o preferencias de usuario. Permiten personalizar la ejecución sin cambiar el código.
</pre>
### Para crear un contenedor con variables de entorno?

```
docker run -d --name <nombre contenedor> -e <nombre variable1>=<valor1> -e <nombre variable2>=<valor2>
```

### Crear un contenedor a partir de la imagen de nginx:alpine con las siguientes variables de entorno: username y role. Para la variable de entorno rol asignar el valor admin.

# COMPLETAR
<pre>
  PS C:\Users\johan> docker run -d --name NginxContainer -e username=myuser -e role=admin nginx:alpine                     
46e2ef1be10eef034cd8e7c6f156005787f5fc9dc126beb1ede67a68c954b910

</pre>

# CAPTURA CON LA COMPROBACIÓN DE LA CREACIÓN DE LAS VARIABLES DE ENTORNO DEL CONTENEDOR ANTERIOR
![image](https://github.com/user-attachments/assets/52ca3015-eb21-401d-9f7c-2279e9c29849)


### Crear un contenedor con mysql:8 , mapear todos los puertos
# COMPLETAR
<pre>
PS C:\Users\johan> docker run -d --name mysqlContainer -e MYSQL_ROOT_PASSWORD=131095 -p 3306:3306 mysql:8          
Unable to find image 'mysql:8' locally
8: Pulling from library/mysql
eba3c26198b7: Pull complete
2b328be7f3cf: Pull complete
dfccffffaa13: Pull complete
39e0a5533d8e: Pull complete
a5394d74c142: Pull complete
9d7dbd4762de: Pull complete
38d47438f1e4: Pull complete
403b4956745f: Pull complete
7cf348cec4fb: Pull complete
d44a5b7781d0: Pull complete
Digest: sha256:bda6ee1f3ae5ebb3cbe9b995c9645ffbd36d7dbda3bd4b4d2ffa43d997073074
Status: Downloaded newer image for mysql:8
db58111485c96bcdc10f1dc47db4fac0a3f33e262cd2868b2619102d705249cc
</pre>

### ¿El contenedor se está ejecutando?
# COMPLETAR

<pre>
PS C:\Users\johan> docker ps
CONTAINER ID   IMAGE                              COMMAND                  CREATED          STATUS          PORTS                                              NAMES
db58111485c9   mysql:8                            "docker-entrypoint.s…"   38 seconds ago   Up 36 seconds   0.0.0.0:3306->3306/tcp, 33060/tcp                  mysqlContainer 
46e2ef1be10e   nginx:alpine                       "/docker-entrypoint.…"   5 minutes ago    Up 5 minutes    80/tcp                                             NginxContainer 
dddf59a707de   jenkins/jenkins:alpine3.18-jdk11   "/sbin/tini -- /usr/…"   32 minutes ago   Up 32 minutes   0.0.0.0:8080->8080/tcp, 0.0.0.0:50000->50000/tcp   JenkinsContenedor
</pre>
<pre>
  El contenedor si se esta ejecutando
</pre>

### Identificar el problema
# COMPLETAR
<pre>
  No hubo problema en mi caso.
</pre>

### Eliminar el contenedor creado con mysql:8 
# COMPLETAR
<pre>
PS C:\Users\johan> docker stop mysqlContainer  
mysqlContainer
PS C:\Users\johan> docker rm mysqlContainer
mysqlContainer
PS C:\Users\johan> docker ps
CONTAINER ID   IMAGE                              COMMAND                  CREATED          STATUS          PORTS                                              NAMES
46e2ef1be10e   nginx:alpine                       "/docker-entrypoint.…"   10 minutes ago   Up 10 minutes   80/tcp                                             NginxContainer
dddf59a707de   jenkins/jenkins:alpine3.18-jdk11   "/sbin/tini -- /usr/…"   37 minutes ago   Up 37 minutes   0.0.0.0:8080->8080/tcp, 0.0.0.0:50000->50000/tcp   JenkinsContenedor
</pre>

### Para crear un contenedor con variables de entorno especificadas
- Portabilidad: Las aplicaciones se vuelven más portátiles y pueden ser desplegadas en diferentes entornos (desarrollo, pruebas, producción) simplemente cambiando el archivo de variables de entorno.
- Centralización: Todas las configuraciones importantes se centralizan en un solo lugar, lo que facilita la gestión y auditoría de las configuraciones.
- Consistencia: Asegura que todos los miembros del equipo de desarrollo o los entornos de despliegue utilicen las mismas configuraciones.
- Evitar Exposición en el Código: Mantener variables sensibles como contraseñas, claves API, y tokens fuera del código fuente reduce el riesgo de exposición accidental a través del control de versiones.
- Control de Acceso: Los archivos de variables de entorno pueden ser gestionados con permisos específicos, limitando quién puede ver o modificar la configuración sensible.

Previo a esto es necesario crear el archivo y colocar las variables en un archivo, **.env** se ha convertido en una convención estándar, pero también es posible usar cualquier extensión como **.txt**.
```
docker run -d --name <nombre contenedor> --env-file=<nombreArchivo>.<extensión> <nombre imagen>
```
**Considerar**
Es necesario especificar la ruta absoluta del archivo si este se encuentra en una ubicación diferente a la que estás ejecutando el comando docker run.

### Crear un contenedor con mysql:8 , mapear todos los puertos y configurar las variables de entorno mediante un archivo
# COMPLETAR
<pre>
 
PS C:\Users\johan> type mysql.env
MYSQL_ROOT_PASSWORD=131095
MYSQL_DATABASE=DBP
MYSQL_USER=PAME
MYSQL_PASSWORD=131095

PS C:\Users\johan>docker run -d --name ContenedorMysql --env-file=mysql.env -p 3306:3306 mysql:8
249987470f4cd55b0f3d7172cb1a3e84bebb7dd91ed748ef44da52567a8b3ad5   
PS C:\Users\johan> 
</pre>

# CAPTURA CON LA COMPROBACIÓN DE LA CREACIÓN DE LAS VARIABLES DE ENTORNO DEL CONTENEDOR ANTERIOR 

![image](https://github.com/user-attachments/assets/cf9bfa15-fe3a-4362-a818-3f175ac0bebb)


### ¿Qué bases de datos existen en el contenedor creado?
# COMPLETAR
<pre>
PS C:\Users\johan> docker exec -it ContenedorMysql mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.4.3 MySQL Community Server - GPL

Copyright (c) 2000, 2024, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| DBP                |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.01 sec)
</pre>

<pre> Hay 5 bases de datos listadas.</pre>
![image](https://github.com/user-attachments/assets/9c6ddc32-9376-40b3-a204-91a183205740)


