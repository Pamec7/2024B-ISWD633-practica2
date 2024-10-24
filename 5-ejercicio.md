## Esquema para el ejercicio
![Imagen](img/esquema-ejercicio5.PNG)

### Crear la red
# COMPLETAR
<pre>
PS C:\Users\johan> docker network create net-wp
d9e05d60d5a3fc016a09c750c608906e4daf9622614e7e5088f6e296dce39ae9
</pre>

### Crear el contenedor mysql a partir de la imagen mysql:8, configurar las variables de entorno necesarias
# COMPLETAR
<pre>
PS C:\Users\johan> docker run -d --name contenedorMysql --network net-wp -e MYSQL_ROOT_PASSWORD=1234 -e MYSQL_DATABASE=wordpress_db  mysql:8 
f2d66caf4253aa7cfe02962ad15e63d3bce8f3a0b95ea2105d4a0b813bc8ba05
</pre>

### Crear el contenedor wordpress a partir de la imagen: wordpress, configurar las variables de entorno necesarias
# COMPLETAR
<pre>
  PS C:\Users\johan>docker run -d --name contenedorWordpress --network net-wp -e WORDPRESS_DB_HOST=contenedorMysql:3306 -e WORDPRESS_DB_NAME=wordpress_db -e WORDPRESS_DB_USER=root -e WORDPRESS_DB_PASSWORD=1234 -p 9300:80 wordpress
c0da28c2f462347ba4e322b27231446ac040d367925359c7d6e8f97ca6437fdb
</pre>

De acuerdo con el trabajo realizado, en la el esquema de ejercicio el puerto a es **(9300)**

Ingresar desde el navegador al wordpress y finalizar la configuración de instalación.
# COLOCAR UNA CAPTURA DE LA CONFIGURACIÓN
![image](https://github.com/user-attachments/assets/6b85e869-a70f-48b0-948f-709826d458f2)
![image](https://github.com/user-attachments/assets/37f7199d-75e9-431c-853c-95e25688a8fa)

Desde el panel de admin: cambiar el tema y crear una nueva publicación.
Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress
# COLOCAR UNA CAPTURA DEL SITO EN DONDE SEA VISIBLE LA PUBLICACIÓN.
![image](https://github.com/user-attachments/assets/dc750a78-2a9a-4d61-8ad4-e4c82c7a70e3)

### Eliminar el contenedor wordpress
# COMPLETAR
<pre>
  PS C:\Users\johan>docker rm -f contenedorWordpress
contenedorWordpress
</pre>
### Crear nuevamente el contenedor wordpress
Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress
<pre>
  PS C:\Users\johan> docker run -d --name contenedorWordpress --network net-wp -e WORDPRESS_DB_HOST=contenedorMysql:3306 -e WORDPRESS_DB_NAME=wordpress_db -e WORDPRESS_DB_USER=root -e WORDPRESS_DB_PASSWORD=1234 -p 9300:80 wordpress
e2f733f4bb1f6cd6bbe77f7e0fe244b983ec40da9d618c0860fe4ae7fccda347
</pre>
### ¿Qué ha sucedido, qué puede observar?
# COMPLETAR
<pre>
Después de recrear el contenedor, los datos de WordPress, incluyendo el tema y las publicaciones, se mantienen intactos. Esto sugiere que WordPress solo actúa como la interfaz de usuario que accede a la base de datos externa en MySQL, de esta manera, los datos persisten fuera del contenedor de la aplicación y se almacenan en una base de datos independiente.
</pre>





