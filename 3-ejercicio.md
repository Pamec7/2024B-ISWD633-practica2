### Crear contenedor de Postgres sin que exponga los puertos. Usar la imagen: postgres:11.21-alpine3.17
# COMPLETAR
<pre>
PS C:\Users\johan> docker run -d --name PostgresContainer -e POSTGRES_PASSWORD=131095 postgres:11.21-alpine3.17              
5b729cfe50449c0b3d10b9cffd9c4e78b4ed1b1bc38ab7a882e709bb7507d70e
</pre>

### Crear un cliente de postgres. Usar la imagen: dpage/pgadmin4

# COMPLETAR
<pre>
PS C:\Users\johan>docker run -d --name AdminContainer -e PGADMIN_DEFAULT_EMAIL=admin@example.com -e PGADMIN_DEFAULT_PASSWORD=131095 -p 80:80 dpage/pgadmin4
2b2e4d26f8735c1abac02e39d363df8b51a6a9ffbb7188572154a0e3023a1f50

</pre>


La figura presenta el esquema creado en donde los puertos son:
- a: (5050)
- b: (80)
- c: (5432)

![Imagen](img/esquema-ejercicio3.PNG)

## Desde el cliente
### Acceder desde el cliente al servidor postgres creado.
# COMPLETAR CON UNA CAPTURA DEL LOGIN
![image](https://github.com/user-attachments/assets/d8573cb9-8d4e-411b-88a7-ed4d076d89ce)

![image](https://github.com/user-attachments/assets/6556acaf-c8a8-4189-a7e8-d699fe6559d4)

### Crear la base de datos info, y dentro de esa base la tabla personas, con id (serial) y nombre (varchar), agregar un par de registros en la tabla, obligatorio incluir su nombre.
## Desde el servidor postgresl
### Acceder al servidor
### Conectarse a la base de datos info
<pre>
  PS C:\Users\johan> docker exec -it PostgresContainer psql -U postgres
psql (11.21)
Type "help" for help.

postgres=# CREATE DATABASE info;
CREATE DATABASE
postgres=# \c info;
You are now connected to database "info" as user "postgres".
info=# CREATE TABLE personas (
info(# id SERIAL PRIMARY KEY,
info(# nombre VARCHAR(100)
info(# );
CREATE TABLE
info=#INSERT INTO personas (nombre) VALUES ('Pamela');
INSERT 0 1
info=#INSERT INTO personas (nombre) VALUES ('Johana');
INSERT 0 1
info=#INSERT INTO personas (nombre) VALUES ('Esteban');
INSERT 0 1
info=#SELECT * FROM personas;
 id | nombre  
----+---------
  1 | Pamela
  2 | Johana
  3 | Esteban
(3 rows)

info=#\q
</pre>

# COMPLETAR
### Realizar un select *from personas
<pre>
  info=#SELECT * FROM personas;
 id | nombre  
----+---------
  1 | Pamela
  2 | Johana
  3 | Esteban
(3 rows)
info=#\q
</pre>
# AGREGAR UNA CAPTURA DE PANTALLA DEL RESULTADO
![image](https://github.com/user-attachments/assets/4cfc0d8c-9365-4d00-a30e-ed3c3792a147)

