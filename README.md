# postgresql
Repositorio personal con Instrucciones y sentencias Pg/Sql para el dia a dia

Obtener Información de la Base de Datos
---------------------------------------

| Descripcion | Comando |
| ------------- | ------------- |
| Bases de datos existentes  | select datname, oid from pg_database;  |
| Numero de conexiones actuales | select count(* ) from pg_stat_activity; |
| Numero maximo de conexiones permitidas  | SHOW max_connections;  |
| Muestra variables de la BD | show all; |
| Muestra la ubicación de la carpeta de datos  | show data_directory;  |
| Obtener la Dirección IP del cliente  | select inet_client_addr();  |
| Version del motor  | select version();  |
| Querys activos  | SELECT  pid, now() - pg_stat_activity.query_start AS duration, query, state FROM pg_stat_activity WHERE (now() - pg_stat_activity.query_start) > interval '1 minutes';   |
|   |   |

