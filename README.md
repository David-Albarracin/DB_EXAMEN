## EXAMEN DATA BASE

Integrantes del Grupo

* JAVIER ANDRES GOMEZ LABRADOR 
* EDGAR BENJAMIN DAVID ALBARRACIN SANABRIA



1. Obtener los nombres de todos los actores y las películas en las
   que han actuado.

   ```sql
   SELECT 
   	a.nombre,
   	a.apellidos,
   	p.titulo AS 'Pelicula'
   FROM pelicula_actor AS pa  
   JOIN pelicula AS p ON p.id_pelicula = pa.id_pelicula 
   JOIN actor AS a ON a.id_actor = pa.id_actor;
   
   +-------------+--------------+-----------------------------+
   | nombre      | apellidos    | Pelicula                    |
   +-------------+--------------+-----------------------------+
   | PENELOPE    | GUINESS      | ACADEMY DINOSAUR            |
   | THORA       | TEMPLE       | WRONG BEHAVIOR              |
   +-------------+--------------+-----------------------------+
   5462 rows in set (0,02 sec)
   
   ```

2. Listar todos los clientes y los almacenes donde están
   registrados.

   ```sql
   SELECT
   	CONCAT(c.nombre, ' ', c.apellidos) AS 'Cliente',
   	c.id_almacen AS 'Almacen id'
   FROM 
   	cliente AS c;
   
   | AUSTIN CINTRON        |          2 |
   | PEPE LÓPEZ            |          2 |
   | MARÍA SÁNCHEZ         |          2 |
   +-----------------------+------------+
   601 rows in set (0,00 sec)
   
   ```

3. Encontrar todas las películas y sus respectivas categorías.

   ```sql
   SELECT 
   	p.titulo AS 'Pelicula',
   	c.nombre AS 'Cateogoria'
   FROM 
   	pelicula_categoria AS pc
   JOIN 
   	categoria AS c ON c.id_categoria = pc.id_categoria
   JOIN 
   	pelicula AS p ON p.id_pelicula = pc.id_pelicula ;
   	
   +-----------------------------+-------------+
   | Pelicula                    | Cateogoria  |
   +-----------------------------+-------------+
   | AMADEUS HOLY                | Action      |
   | AMERICAN CIRCUS             | Action      |
   | WORKER TARZAN               | Travel      |
   | WORKING MICROCOSMOS         | Travel      |
   +-----------------------------+-------------+
   1000 rows in set (0,00 sec)
   ```

4. Listar los nombres de las ciudades junto con sus países.

   ```sql
   SELECT DISTINCT( 
   	c.nombre) AS 'Ciudad',
   	p.nombre AS 'Pais'
   FROM 
   	ciudad AS c
   JOIN
   	pais AS p ON p.id_pais = c.id_pais ;
   	
   | Novi Sad                   | Yugoslavia                            |
   | Kitwe                      | Zambia                                |
   +----------------------------+---------------------------------------+
   600 rows in set (0,00 sec)
   
   ```

5. Obtener los detalles de los alquileres, incluyendo el cliente y el
   empleado que gestionó el alquiler.

   ```sql
   SELECT 
   	a.id_alquiler,
   	c.nombre,
   	e.nombre 
   FROM
   	alquiler AS a 
   JOIN 
   	cliente AS c ON c.id_cliente = a.id_cliente 
   JOIN 
   	empleado AS e ON e.id_empleado = a.id_empleado ;
   	
   |       15719 | AUSTIN      | Mike   |
   |       15725 | AUSTIN      | Mike   |
   +-------------+-------------+--------+
   16045 rows in set (0,04 sec)
   
   ```

6. Encontrar todas las películas que se encuentran en un almacén
   específico.

   ```sql
   SELECT
   	i.id_almacen,
   	COUNT(i.id_pelicula) AS 'n_peliculas' 
   FROM 
   	inventario AS i
   GROUP BY
   	i.id_almacen;
   
   +------------+-------------+
   | id_almacen | n_peliculas |
   +------------+-------------+
   |          1 |        2270 |
   |          2 |        2311 |
   +------------+-------------+
   2 rows in set (0,00 sec)
   
   ```

7. Listar los nombres y apellidos de los empleados junto con las
   direcciones de los almacenes en los que trabajan.

   ```sql
   SELECT 
   	CONCAT(e.nombre, ' ', e.apellidos) AS 'Empleado',
   	d.direccion AS 'Direccion',
   	a.id_almacen AS 'Almacen'
   FROM 
   	empleado AS e
   JOIN
   	almacen AS a ON a.id_almacen = e.id_almacen 
   JOIN 
   	direccion AS d ON d.id_direccion = a.id_direccion;  
   	
   +---------------+--------------------+---------+
   | Empleado      | Direccion          | Almacen |
   +---------------+--------------------+---------+
   | Mike Hillyer  | 28 MySQL Boulevard |       2 |
   | Jon Stephens  | 28 MySQL Boulevard |       2 |
   | Pepe Spilberg | 28 MySQL Boulevard |       2 |
   | Ada Byron     | 47 MySakila Drive  |       1 |
   | Ringo Rooksby | 47 MySakila Drive  |       1 |
   +---------------+--------------------+---------+
   5 rows in set (0,00 sec)
   ```

8. Obtener una lista de pagos realizados, incluyendo el cliente, el
   empleado que registró el pago y el alquiler correspondiente.

   ```sql
   SELECT
   	p.id_pago,
   	CONCAT(c.nombre, ' ', c.apellidos) AS 'Cliente',
   	CONCAT(e.nombre, ' ', e.apellidos) AS 'Empleado'
   FROM 
   	pago AS p
   JOIN
   	cliente AS c ON c.id_cliente = p.id_cliente 
   JOIN 
   	empleado AS e ON e.id_empleado = p.id_empleado;
   	
   	
   |   16048 | AUSTIN CINTRON        | Jon Stephens |
   |   16049 | AUSTIN CINTRON        | Jon Stephens |
   +---------+-----------------------+--------------+
   16049 rows in set (0,03 sec)
   
   ```

9. Listar las películas y los idiomas en los que están disponibles.

   ```sql
   SELECT 
   	p.titulo,
   	i.nombre 
   FROM 
   	pelicula AS p
   JOIN
   	idioma AS i ON i.id_idioma = p.id_idioma;
   	
   /*
   SIN IDIOMAS DISPONIBLES 
   
   SELECT 
   	p.titulo,
   	i.nombre 
   FROM 
   	pelicula AS p
   LEFT JOIN
   	idioma AS i ON i.id_idioma = p.id_idioma;
   
   */	
   	
   +-----------------------------+---------+
   | titulo                      | nombre  |
   +-----------------------------+---------+
   | ACADEMY DINOSAUR            | English |
   | ACE GOLDFINGER              | English |
   | ZHIVAGO CORE                | English |
   | ZOOLANDER FICTION           | English |
   | ZORRO ARK                   | English |
   +-----------------------------+---------+
   1000 rows in set (0,00 sec)
   
   ```

10. Encontrar todos los empleados y los almacenes que gestionan.

    ```sql
    SELECT 
    	e.nombre AS 'Empleado',
    	a.id_almacen
    FROM 
    	empleado AS e
    JOIN
    	almacen AS a ON a.id_empleado_jefe = e.id_empleado;
    	
    +----------+------------+
    | Empleado | id_almacen |
    +----------+------------+
    | Jon      |          2 |
    | Ringo    |          1 |
    +----------+------------+
    2 rows in set (0,00 sec)
    
    ```

11. Obtener los títulos de las películas que nunca han sido
    alquiladas.

    ```sql
    SELECT 
    	p.titulo,
    	a.id_alquiler
    FROM 
    	pelicula AS p
    LEFT JOIN
    	inventario AS i ON i.id_pelicula  = p.id_pelicula  
    LEFT JOIN 
    	alquiler AS a ON a.id_inventario = i.id_inventario 
    WHERE 
    	a.id_inventario IS NULL;
    	
    +------------------------+-------------+
    | titulo                 | id_alquiler |
    +------------------------+-------------+
    | ACADEMY DINOSAUR       |        NULL |
    | ALICE FANTASIA         |        NULL |
    | APOLLO TEEN            |        NULL |
    | ARGONAUTS TOWN         |        NULL |
    | VILLAIN DESPERATE      |        NULL |
    | VOLUME HOUSE           |        NULL |
    | WAKE JAWS              |        NULL |
    | WALLS ARTIST           |        NULL |
    +------------------------+-------------+
    43 rows in set (0,01 sec)
    
    
    ```

12. Listar los empleados que trabajan en el mismo almacén que el
    empleado con id_empleado = 1. -

    ```sql
    SELECT 
    	e2.nombre,
    	e2.id_almacen
    FROM 
    	empleado AS e
    JOIN
    	empleado AS e2 ON e2.id_almacen = e.id_almacen
    WHERE 
    	e.id_empleado = 1;
    	
    +--------+------------+
    | nombre | id_almacen |
    +--------+------------+
    | Mike   |          2 |
    | Jon    |          2 |
    | Pepe   |          2 |
    +--------+------------+
    3 rows in set (0,00 sec)
    
    
    ```

13. Encontrar el nombre de las ciudades que no tienen ningún
    cliente registrado.

    ```sql
    SELECT 
    	c.nombre 
    FROM 
    	ciudad AS c
    LEFT JOIN
    	direccion AS d ON d.id_ciudad = c.id_ciudad
    LEFT JOIN 
    	cliente AS c2 ON c2.id_direccion = d.id_direccion  
    WHERE 
    	d.id_ciudad IS NULL
    	AND 
    	c2.id_direccion IS NULL
    	;
    	
    +----------------------------+
    | nombre                     |
    +----------------------------+
    | A Corua (La Corua)         |	
    | Zhoushan                   |
    | Ziguinchor                 |
    +----------------------------+
    558 rows in set (0,00 sec)
    
    ```

14. Obtener los nombres y apellidos de los actores que han
    participado en más de 10 películas.(having)

    ```sql
    SELECT
    	a.nombre,
    	COUNT(pa.id_pelicula) AS 'n_Pelicuas' 
    FROM 
    	pelicula_actor AS pa
    JOIN
     	actor AS a ON a.id_actor = pa.id_actor 
    GROUP BY 
    	a.nombre 
    HAVING 
     	n_Pelicuas > 10;
     	
    +-------------+------------+
    | nombre      | n_Pelicuas |
    +-------------+------------+
    | PENELOPE    |        102 |
    | BELA        |         30 |
    | THORA       |         20 |
    +-------------+------------+
    128 rows in set (0,01 sec)
    
    ```

15. Encontrar los nombres y apellidos de los clientes que han
    realizado un pago mayor a 100.

    ```sql
    SELECT
    	c.nombre,
    	c.apellidos
    FROM 
    	pago AS p
    JOIN
    	cliente AS c ON c.id_cliente = p.id_cliente 
    WHERE 
    	p.total > 100;
    	
    	
    Empty set (0,01 sec)
    ```

16. Listar los títulos de las películas lanzadas en el mismo año que
    la película con id_pelicula = 2.

    ```sql
    SELECT 
    	p2.titulo,
    FROM 
    	pelicula AS p
    JOIN
    	pelicula AS p2 ON p2.anyo_lanzamiento = p.anyo_lanzamiento 
    WHERE 
    	p.id_pelicula = 2;
    	
    +-----------------------------+
    | titulo                      |
    +-----------------------------+
    | ACADEMY DINOSAUR            |
    | ZORRO ARK                   |
    +-----------------------------+
    1000 rows in set (0,00 sec)
    ```

    
