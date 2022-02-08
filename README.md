# PostgreSql
Repositorio personal con Instrucciones y sentencias Pg/Sql para el dia a dia

Obtener Información de la Base de Datos
---------------------------------------

| Descripcion                | Comando                                |
| -------------------------- | -------------------------------------- |
| Bases de datos existentes  | SELECT datname, oid FROM pg_database;  |
| Dirección IP del cliente  | SELECT inet_client_addr();  |
| Numero de conexiones actuales | SELECT count(* ) FROM pg_stat_activity; |
| Numero maximo de conexiones permitidas  | SHOW max_connections;  |
| Querys activos  | SELECT  pid, now() - pg_stat_activity.query_start AS duration, query, state <br>FROM pg_stat_activity WHERE (now() - pg_stat_activity.query_start) > interval '1 minutes';  |
| Listar los limites de tamaños de la BD | SELECT * FROM information_schema.sql_sizing; |
| Listar las tablas de la BD | SELECT table_name, table_catalog FROM information_schema.tables <br>WHERE table_schema = 'public' <br>and table_catalog='Nombre_BD' |
| Listar el tamaño de las tablas | SELECT table_name, pg_relation_size(quote_ident(table_name)) <br>FROM information_schema.tables <br>WHERE table_schema = 'public' AND table_catalog='Nombre_BD' ORDER BY 2  |
| Listar las funciones | SELECT routine_name  FROM information_schema.routines <br>WHERE routine_schema = 'public' AND specific_catalog='Nombre_BD' |
| Listar las secuencias | SELECT sequence_name  FROM information_schema.sequences <br>WHERE sequence_schema = 'public' AND sequence_catalog='Nombre_BD' |
| Tamaño de la BD |  SELECT pg_size_pretty( pg_database_size('Nombre_BD') ); |
| Ubicación de la carpeta de datos  | show data_directory;  |
| Ubicacion del archivo pg_hba.conf | show hba_file; |
| Ubicacion fisica de una tabla | SELECT pg_relation_filepath('Nombre_Table'); |
| Variables de la BD | show all; |
| Version del motor  | SELECT version();  |
 
Copia de Seguridad
---------------------------------------

| Descripcion                | Comando                                |
| -------------------------- | -------------------------------------- |
| Dump a archivo .sql | #pg_dump -U postgres Nombre_BD > nombre_archivo.sql  |
| Dump solo esquema a archivo .sql | #pg_dump -U postgres Nombre_BD  --schema-only > nombre_archivo.sql |
| Dump solo una tabla | #pg_dump -U postgres  Nombre_BD  --table  nombre_tabla > nombre_archivo.sql |
| Dump a formato tar | #pg_dump -U postgres -o -Ft Nombre_BD > nombre_archivo.tar |
| Restaurar desde archivo .sql | #psql -U username -d database_name -f nombre_archivo.sql|
| restaurar desde archivo .tar con Log de suceso | #pg_restore -d Nombre_BD -U postgres -p 5433 -Ft -v nombre_archivo.tar > logsucesos.txt 2>&1  |

