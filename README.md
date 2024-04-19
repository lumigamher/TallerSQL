# Taller de SQL en MySQL

## Crear DB y sus tablas 

Para crear la base de datos y las tablas, puedes seguir estos pasos:

1. Crear la base de datos:

```sql
CREATE DATABASE GestorEmpleados;
```

2. Usar la base de datos creada:

```sql
USE GestorEmpleados;
```

3. Crear la tabla `departamento`:

```sql
CREATE TABLE departamento (
    id_departamento INT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    presupuesto INT NOT NULL,
    gastos INT NOT NULL
);
```

4. Crear la tabla `empleado`:

```sql
CREATE TABLE empleado (
    id_empleado INT PRIMARY KEY,
    nif VARCHAR(9) UNIQUE NOT NULL,
    nombre VARCHAR(100) NOT NULL,
    apellido1 VARCHAR(100) NOT NULL,
    apellido2 VARCHAR(100),
    id_departamento INT NULL,
    FOREIGN KEY (id_departamento) REFERENCES departamento(id_departamento)
);
```

5. Insertar los datos de ejemplo proporcionados en el enunciado:

```sql
INSERT INTO departamento VALUES(1, 'Desarrollo', 120000, 6000);
INSERT INTO departamento VALUES(2, 'Sistemas', 150000, 21000);
INSERT INTO departamento VALUES(3, 'Recursos Humanos', 280000, 25000);
INSERT INTO departamento VALUES(4, 'Contabilidad', 110000, 3000);
INSERT INTO departamento VALUES(5, 'I+D', 375000, 380000);
INSERT INTO departamento VALUES(6, 'Proyectos', 0, 0);
INSERT INTO departamento VALUES(7, 'Publicidad', 0, 1000);

INSERT INTO empleado VALUES(1, '32481596F', 'Aarón', 'Rivero', 'Gómez', 1);
INSERT INTO empleado VALUES(2, 'Y5575632D', 'Adela', 'Salas', 'Díaz', 2);
INSERT INTO empleado VALUES(3, 'R6970642B', 'Adolfo', 'Rubio', 'Flores', 3);
INSERT INTO empleado VALUES(4, '77705545E', 'Adrián', 'Suárez', NULL, 4);
INSERT INTO empleado VALUES(5, '17087203C', 'Marcos', 'Loyola', 'Méndez', 5);
INSERT INTO empleado VALUES(6, '38382980M', 'María', 'Santana', 'Moreno', 1);
INSERT INTO empleado VALUES(7, '80576669X', 'Pilar', 'Ruiz', NULL, 2);
INSERT INTO empleado VALUES(8, '71651431Z', 'Pepe', 'Ruiz', 'Santana', 3);
INSERT INTO empleado VALUES(9, '56399183D', 'Juan', 'Gómez', 'López', 2);
INSERT INTO empleado VALUES(10, '46384486H', 'Diego','Flores', 'Salas', 5);
INSERT INTO empleado VALUES(11, '67389283A', 'Marta','Herrera', 'Gil', 1);
INSERT INTO empleado VALUES(12, '41234836R', 'Irene','Salas', 'Flores', NULL);
INSERT INTO empleado VALUES(13, '82635162B', 'Juan Antonio','Sáez', 'Guerrero', NULL);
```

## Consultas sobre una tabla

1. Lista el primer apellido de todos los empleados.

```sql
SELECT apellido1 FROM empleado;
```

```sql
+-----------+
| apellido1 |
+-----------+
| Rivero    |
| Salas     |
| Rubio     |
| Suárez    |
| Loyola    |
| Santana   |
| Ruiz      |
| Ruiz      |
| Gómez     |
| Flores    |
| Herrera   |
| Salas     |
| Sáez      |
+-----------+
13 rows in set (0,00 sec)
```

2. Lista el primer apellido de los empleados eliminando los apellidos que estén repetidos.

```sql
SELECT DISTINCT apellido1 FROM empleado;

+-----------+
| apellido1 |
+-----------+
| Rivero    |
| Salas     |
| Rubio     |
| Suárez    |
| Loyola    |
| Santana   |
| Ruiz      |
| Gómez     |
| Flores    |
| Herrera   |
| Sáez      |
+-----------+
11 rows in set (0,02 sec)
```

3. Lista todas las columnas de la tabla empleado.
```sql
SELECT id_empleado, nif, nombre, apellido1, apellido2 FROM empleado;

+-------------+-----------+--------------+-----------+-----------+
| id_empleado | nif       | nombre       | apellido1 | apellido2 |
+-------------+-----------+--------------+-----------+-----------+
|           1 | 32481596F | Aarón        | Rivero    | Gómez     |
|           2 | Y5575632D | Adela        | Salas     | Díaz      |
|           3 | R6970642B | Adolfo       | Rubio     | Flores    |
|           4 | 77705545E | Adrián       | Suárez    | NULL      |
|           5 | 17087203C | Marcos       | Loyola    | Méndez    |
|           6 | 38382980M | María        | Santana   | Moreno    |
|           7 | 80576669X | Pilar        | Ruiz      | NULL      |
|           8 | 71651431Z | Pepe         | Ruiz      | Santana   |
|           9 | 56399183D | Juan         | Gómez     | López     |
|          10 | 46384486H | Diego        | Flores    | Salas     |
|          11 | 67389283A | Marta        | Herrera   | Gil       |
|          12 | 41234836R | Irene        | Salas     | Flores    |
|          13 | 82635162B | Juan Antonio | Sáez      | Guerrero  |
+-------------+-----------+--------------+-----------+-----------+
13 rows in set (0,00 sec)
```

 4. Lista el nombre y los apellidos de todos los empleados.
```sql
SELECT nombre, apellido1, apellido2 FROM empleado;

+--------------+-----------+-----------+
| nombre       | apellido1 | apellido2 |
+--------------+-----------+-----------+
| Aarón        | Rivero    | Gómez     |
| Adela        | Salas     | Díaz      |
| Adolfo       | Rubio     | Flores    |
| Adrián       | Suárez    | NULL      |
| Marcos       | Loyola    | Méndez    |
| María        | Santana   | Moreno    |
| Pilar        | Ruiz      | NULL      |
| Pepe         | Ruiz      | Santana   |
| Juan         | Gómez     | López     |
| Diego        | Flores    | Salas     |
| Marta        | Herrera   | Gil       |
| Irene        | Salas     | Flores    |
| Juan Antonio | Sáez      | Guerrero  |
+--------------+-----------+-----------+
13 rows in set (0,00 sec)
```

 5. Lista el identificador de los departamentos de los empleados que aparecen en la tabla empleado.
```sql
SELECT id_departamento FROM empleado;

+-----------------+
| id_departamento |
+-----------------+
|            NULL |
|            NULL |
|               1 |
|               1 |
|               1 |
|               2 |
|               2 |
|               2 |
|               3 |
|               3 |
|               4 |
|               5 |
|               5 |
+-----------------+
13 rows in set (0,00 sec)
```

 6. Lista el identificador de los departamentos de los empleados que aparecen en la tabla empleado, eliminando los identificadores que aparecen repetidos.
```sql
SELECT DISTINCT id_departamento FROM empleado;

+-----------------+
| id_departamento |
+-----------------+
|            NULL |
|               1 |
|               2 |
|               3 |
|               4 |
|               5 |
+-----------------+
6 rows in set (0,00 sec)
```

 7. Lista el nombre y apellidos de los empleados en una única columna.
```sql
SELECT CONCAT_WS(' ',nombre, apellido1, apellido2) AS NombreCompleto FROM empleado;
+-----------------------------+
| NombreCompleto              |
+-----------------------------+
| Aarón Rivero Gómez          |
| Adela Salas Díaz            |
| Adolfo Rubio Flores         |
| Adrián Suárez               |
| Marcos Loyola Méndez        |
| María Santana Moreno        |
| Pilar Ruiz                  |
| Pepe Ruiz Santana           |
| Juan Gómez López            |
| Diego Flores Salas          |
| Marta Herrera Gil           |
| Irene Salas Flores          |
| Juan Antonio Sáez Guerrero  |
+-----------------------------+
13 rows in set (0,00 sec)
```

 8. Lista el nombre y apellidos de los empleados en una única columna, convirtiendo todos los caracteres en mayúscula.
```sql
SELECT UPPER(CONCAT_WS(' ',nombre, apellido1, apellido2))AS NombreCompleto FROM empleado;
+-----------------------------+
| NombreCompleto              |
+-----------------------------+
| AARÓN RIVERO GÓMEZ          |
| ADELA SALAS DÍAZ            |
| ADOLFO RUBIO FLORES         |
| ADRIÁN SUÁREZ               |
| MARCOS LOYOLA MÉNDEZ        |
| MARÍA SANTANA MORENO        |
| PILAR RUIZ                  |
| PEPE RUIZ SANTANA           |
| JUAN GÓMEZ LÓPEZ            |
| DIEGO FLORES SALAS          |
| MARTA HERRERA GIL           |
| IRENE SALAS FLORES          |
| JUAN ANTONIO SÁEZ GUERRERO  |
+-----------------------------+
13 rows in set (0,00 sec)
```

 9. Lista el nombre y apellidos de los empleados en una única columna, convirtiendo todos los caracteres en minúscula.
```sql
SELECT LOWER(CONCAT_WS(' ',nombre, apellido1, apellido2))AS NombreCompleto FROM empleado;
+-----------------------------+
| NombreCompleto              |
+-----------------------------+
| aarón rivero gómez          |
| adela salas díaz            |
| adolfo rubio flores         |
| adrián suárez               |
| marcos loyola méndez        |
| maría santana moreno        |
| pilar ruiz                  |
| pepe ruiz santana           |
| juan gómez lópez            |
| diego flores salas          |
| marta herrera gil           |
| irene salas flores          |
| juan antonio sáez guerrero  |
+-----------------------------+
13 rows in set (0,00 sec)
```

 10. Lista el identificador de los empleados junto al nif, pero el nif deberá aparecer en dos columnas, una mostrará únicamente los dígitos del nif y la otra la letra.
```sql
SELECT id_empleado, SUBSTRING(nif, 1, LENGTH(nif) - 1) AS digitos_nif, SUBSTRING(nif, LENGTH(nif), 1) AS letra_nif FROM empleado;

+-------------+-------------+-----------+
| id_empleado | digitos_nif | letra_nif |
+-------------+-------------+-----------+
|           5 | 17087203    | C         |
|           1 | 32481596    | F         |
|           6 | 38382980    | M         |
|          12 | 41234836    | R         |
|          10 | 46384486    | H         |
|           9 | 56399183    | D         |
|          11 | 67389283    | A         |
|           8 | 71651431    | Z         |
|           4 | 77705545    | E         |
|           7 | 80576669    | X         |
|          13 | 82635162    | B         |
|           3 | R6970642    | B         |
|           2 | Y5575632    | D         |
+-------------+-------------+-----------+
13 rows in set (0,00 sec)
```

 11. Lista el nombre de cada departamento y el valor del presupuesto actual del que dispone. Para calcular este dato tendrá que restar al valor del presupuesto inicial (columna presupuesto) los gastos que se han generado (columna gastos). Tenga en cuenta que en algunos casos pueden existir valores negativos. Utilice un alias apropiado para la nueva columna columna que está calculando.
```sql
SELECT d.nombre, (d.presupuesto - d.gastos) AS presupuesto_actual FROM departamento d;

+------------------+--------------------+
| nombre           | presupuesto_actual |
+------------------+--------------------+
| Desarrollo       |             114000 |
| Sistemas         |             129000 |
| Recursos Humanos |             255000 |
| Contabilidad     |             107000 |
| I+D              |              -5000 |
| Proyectos        |                  0 |
| Publicidad       |              -1000 |
+------------------+--------------------+
7 rows in set (0,00 sec)
```

 12. Lista el nombre de los departamentos y el valor del presupuesto actual ordenado de forma ascendente.
```sql
SELECT d.nombre, (d.presupuesto - d.gastos) AS presupuesto_actual FROM departamento d ORDER BY presupuesto_actual ASC;

+------------------+--------------------+
| nombre           | presupuesto_actual |
+------------------+--------------------+
| I+D              |              -5000 |
| Publicidad       |              -1000 |
| Proyectos        |                  0 |
| Contabilidad     |             107000 |
| Desarrollo       |             114000 |
| Sistemas         |             129000 |
| Recursos Humanos |             255000 |
+------------------+--------------------+
7 rows in set (0,00 sec)
```

 13. Lista el nombre de todos los departamentos ordenados de forma ascendente.
```sql
SELECT d.nombre FROM departamento d ORDER BY d.nombre ASC;

+------------------+
| nombre           |
+------------------+
| Contabilidad     |
| Desarrollo       |
| I+D              |
| Proyectos        |
| Publicidad       |
| Recursos Humanos |
| Sistemas         |
+------------------+
7 rows in set (0,00 sec)
```

 14. Lista el nombre de todos los departamentos ordenados de forma descendente.
```sql
SELECT d.nombre FROM departamento d ORDER BY d.nombre DESC;

+------------------+
| nombre           |
+------------------+
| Sistemas         |
| Recursos Humanos |
| Publicidad       |
| Proyectos        |
| I+D              |
| Desarrollo       |
| Contabilidad     |
+------------------+
7 rows in set (0,00 sec)
```

 15. Lista los apellidos y el nombre de todos los empleados, ordenados de forma alfabética tendiendo en cuenta en primer lugar sus apellidos y luego su nombre.
```sql
SELECT e.apellido1, e.apellido2, e.nombre FROM empleado e ORDER BY e.apellido1, e.nombre;

+-----------+-----------+--------------+
| apellido1 | apellido2 | nombre       |
+-----------+-----------+--------------+
| Flores    | Salas     | Diego        |
| Gómez     | López     | Juan         |
| Herrera   | Gil       | Marta        |
| Loyola    | Méndez    | Marcos       |
| Rivero    | Gómez     | Aarón        |
| Rubio     | Flores    | Adolfo       |
| Ruiz      | Santana   | Pepe         |
| Ruiz      | NULL      | Pilar        |
| Sáez      | Guerrero  | Juan Antonio |
| Salas     | Díaz      | Adela        |
| Salas     | Flores    | Irene        |
| Santana   | Moreno    | María        |
| Suárez    | NULL      | Adrián       |
+-----------+-----------+--------------+
13 rows in set (0,00 sec)
```

 16. Devuelve una lista con el nombre y el presupuesto, de los 3 departamentos que tienen mayor presupuesto.
```sql
SELECT d.nombre, d.presupuesto FROM departamento d ORDER BY d.presupuesto DESC LIMIT 3;

+------------------+-------------+
| nombre           | presupuesto |
+------------------+-------------+
| I+D              |      375000 |
| Recursos Humanos |      280000 |
| Sistemas         |      150000 |
+------------------+-------------+
3 rows in set (0,00 sec)
```

 17. Devuelve una lista con el nombre y el presupuesto, de los 3 departamentos que tienen menor presupuesto.
```sql
SELECT d.nombre, d.presupuesto FROM departamento d ORDER BY d.presupuesto ASC LIMIT 3;

+--------------+-------------+
| nombre       | presupuesto |
+--------------+-------------+
| Proyectos    |           0 |
| Publicidad   |           0 |
| Contabilidad |      110000 |
+--------------+-------------+
3 rows in set (0,00 sec)
```

 18. Devuelve una lista con el nombre y el gasto, de los 2 departamentos que tienen mayor gasto.
```sql
SELECT d.nombre, d.gastos FROM departamento d ORDER BY d.gastos DESC LIMIT 2;

+------------------+--------+
| nombre           | gastos |
+------------------+--------+
| I+D              | 380000 |
| Recursos Humanos |  25000 |
+------------------+--------+
2 rows in set (0,00 sec)
```

 19. Devuelve una lista con el nombre y el gasto, de los 2 departamentos que tienen menor gasto.
```sql
SELECT d.nombre, d.gastos FROM departamento d ORDER BY d.gastos ASC LIMIT 2;

+------------+--------+
| nombre     | gastos |
+------------+--------+
| Proyectos  |      0 |
| Publicidad |   1000 |
+------------+--------+
2 rows in set (0,00 sec)
```

 20. Devuelve una lista con 5 filas a partir de la tercera fila de la tabla empleado. La tercera fila se debe incluir en la respuesta. La respuesta debe incluir todas las columnas de la tabla empleado.
```sql
SELECT id_empleado, nif, nombre, apellido1, apellido2 FROM empleado LIMIT 5 OFFSET 2;

+-------------+-----------+---------+-----------+-----------+
| id_empleado | nif       | nombre  | apellido1 | apellido2 |
+-------------+-----------+---------+-----------+-----------+
|           3 | R6970642B | Adolfo  | Rubio     | Flores    |
|           4 | 77705545E | Adrián  | Suárez    | NULL      |
|           5 | 17087203C | Marcos  | Loyola    | Méndez    |
|           6 | 38382980M | María   | Santana   | Moreno    |
|           7 | 80576669X | Pilar   | Ruiz      | NULL      |
+-------------+-----------+---------+-----------+-----------+
5 rows in set (0,00 sec)
```

 21. Devuelve una lista con el nombre de los departamentos y el presupuesto, de aquellos que tienen un presupuesto mayor o igual a 150000 euros.
```sql
SELECT d.nombre, d.presupuesto FROM departamento d WHERE d.presupuesto >= 150000;

+------------------+-------------+
| nombre           | presupuesto |
+------------------+-------------+
| Sistemas         |      150000 |
| Recursos Humanos |      280000 |
| I+D              |      375000 |
+------------------+-------------+
3 rows in set (0,00 sec)
```

 22. Devuelve una lista con el nombre de los departamentos y el gasto, de aquellos que tienen menos de 5000 euros de gastos. 
```sql
SELECT d.nombre, d.gastos FROM departamento d WHERE d.gastos < 5000;

+--------------+--------+
| nombre       | gastos |
+--------------+--------+
| Contabilidad |   3000 |
| Proyectos    |      0 |
| Publicidad   |   1000 |
+--------------+--------+
3 rows in set (0,00 sec)
```

 23. Devuelve una lista con el nombre de los departamentos y el presupuesto, de aquellos que tienen un presupuesto entre 100000 y 200000 euros. Sin utilizar el operador BETWEEN.
```sql
SELECT d.nombre, d.presupuesto FROM departamento d WHERE d.presupuesto > 100000 AND d.presupuesto < 200000;

+--------------+-------------+
| nombre       | presupuesto |
+--------------+-------------+
| Desarrollo   |      120000 |
| Sistemas     |      150000 |
| Contabilidad |      110000 |
+--------------+-------------+
3 rows in set (0,00 sec)
```

 24. Devuelve una lista con el nombre de los departamentos que no tienen un presupuesto entre 100000 y 200000 euros. Sin utilizar el operador BETWEEN.
```sql
SELECT d.nombre FROM departamento d WHERE d.presupuesto < 100000 OR d.presupuesto > 200000;

+------------------+-------------+
| nombre           | presupuesto |
+------------------+-------------+
| Desarrollo       |      120000 |
| Sistemas         |      150000 |
| Recursos Humanos |      280000 |
| Contabilidad     |      110000 |
| I+D              |      375000 |
| Proyectos        |           0 |
| Publicidad       |           0 |
+------------------+-------------+
7 rows in set (0,00 sec)
```

25.Devuelve una lista con el nombre de los departamentos que tienen un presupuesto entre 100000 y 200000 euros. Utilizando el operador BETWEEN.

```sql
SELECT d.nombre, d.presupuesto FROM departamento d WHERE d.presupuesto BETWEEN 100000 AND 200000;

+--------------+-------------+
| nombre       | presupuesto |
+--------------+-------------+
| Desarrollo   |      120000 |
| Sistemas     |      150000 |
| Contabilidad |      110000 |
+--------------+-------------+
3 rows in set (0,00 sec)
```

 26. Devuelve una lista con el nombre de los departamentos que no tienen un presupuesto entre 100000 y 200000 euros. Utilizando el operador BETWEEN.
```sql
SELECT d.nombre FROM departamento d WHERE d.presupuesto NOT BETWEEN 100000 AND 200000;

+------------------+-------------+
| nombre           | presupuesto |
+------------------+-------------+
| Recursos Humanos |      280000 |
| I+D              |      375000 |
| Proyectos        |           0 |
| Publicidad       |           0 |
+------------------+-------------+
4 rows in set (0,00 sec)
```

 27. Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean mayores que el presupuesto del que disponen.
```sql
SELECT d.nombre, d.gastos, d.presupuesto FROM departamento d WHERE d.gastos > d.presupuesto;

+------------+--------+-------------+
| nombre     | gastos | presupuesto |
+------------+--------+-------------+
| I+D        | 380000 |      375000 |
| Publicidad |   1000 |           0 |
+------------+--------+-------------+
2 rows in set (0,00 sec)
```

 28. Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean menores que el presupuesto del que disponen.
```sql
SELECT d.nombre, d.gastos, d.presupuesto FROM departamento d WHERE d.gastos < d.presupuesto;

+------------------+--------+-------------+
| nombre           | gastos | presupuesto |
+------------------+--------+-------------+
| Desarrollo       |   6000 |      120000 |
| Sistemas         |  21000 |      150000 |
| Recursos Humanos |  25000 |      280000 |
| Contabilidad     |   3000 |      110000 |
+------------------+--------+-------------+
4 rows in set (0,00 sec)
```

 29. Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean iguales al presupuesto del que disponen.
```sql
SELECT d.nombre, d.gastos, d.presupuesto FROM departamento d WHERE d.gastos = d.presupuesto;

+-----------+--------+-------------+
| nombre    | gastos | presupuesto |
+-----------+--------+-------------+
| Proyectos |      0 |           0 |
+-----------+--------+-------------+
1 row in set (0,00 sec)
```

 30. Lista todos los datos de los empleados cuyo segundo apellido sea NULL.
```sql
SELECT id_empleado, nif, nombre, apellido1, apellido2 FROM empleado WHERE apellido2 IS NULL;

+-------------+-----------+---------+-----------+-----------+
| id_empleado | nif       | nombre  | apellido1 | apellido2 |
+-------------+-----------+---------+-----------+-----------+
|           4 | 77705545E | Adrián  | Suárez    | NULL      |
|           7 | 80576669X | Pilar   | Ruiz      | NULL      |
+-------------+-----------+---------+-----------+-----------+
2 rows in set (0,00 sec)
```

 31. Lista todos los datos de los empleados cuyo segundo apellido no sea NULL.
```sql
SELECT id_empleado, nif, nombre, apellido1, apellido2 FROM empleado WHERE apellido2 IS NOT NULL;

+-------------+-----------+--------------+-----------+-----------+
| id_empleado | nif       | nombre       | apellido1 | apellido2 |
+-------------+-----------+--------------+-----------+-----------+
|           1 | 32481596F | Aarón        | Rivero    | Gómez     |
|           2 | Y5575632D | Adela        | Salas     | Díaz      |
|           3 | R6970642B | Adolfo       | Rubio     | Flores    |
|           5 | 17087203C | Marcos       | Loyola    | Méndez    |
|           6 | 38382980M | María        | Santana   | Moreno    |
|           8 | 71651431Z | Pepe         | Ruiz      | Santana   |
|           9 | 56399183D | Juan         | Gómez     | López     |
|          10 | 46384486H | Diego        | Flores    | Salas     |
|          11 | 67389283A | Marta        | Herrera   | Gil       |
|          12 | 41234836R | Irene        | Salas     | Flores    |
|          13 | 82635162B | Juan Antonio | Sáez      | Guerrero  |
+-------------+-----------+--------------+-----------+-----------+
11 rows in set (0,00 sec)
```

 32. Lista todos los datos de los empleados cuyo segundo apellido sea 'López'.
```sql
SELECT id_empleado, nif, nombre, apellido1, apellido2 FROM empleado WHERE apellido2 = 'López';

+-------------+-----------+--------+-----------+-----------+
| id_empleado | nif       | nombre | apellido1 | apellido2 |
+-------------+-----------+--------+-----------+-----------+
|           9 | 56399183D | Juan   | Gómez     | López     |
+-------------+-----------+--------+-----------+-----------+
1 row in set (0,00 sec)
```

 33. Lista todos los datos de los empleados cuyo segundo apellido sea 'Díaz' o 'Moreno'. Sin utilizar el operador IN.
```sql
SELECT id_empleado, nif, nombre, apellido1, apellido2 FROM empleado WHERE apellido2 = 'Díaz' OR apellido2 = 'Moreno';

+-------------+-----------+--------+-----------+-----------+
| id_empleado | nif       | nombre | apellido1 | apellido2 |
+-------------+-----------+--------+-----------+-----------+
|           2 | Y5575632D | Adela  | Salas     | Díaz      |
|           6 | 38382980M | María  | Santana   | Moreno    |
+-------------+-----------+--------+-----------+-----------+
2 rows in set (0,00 sec)
```

 34. Lista todos los datos de los empleados cuyo segundo apellido sea 'Díaz' o 'Moreno'. Utilizando el operador IN.
```sql
SELECT id_empleado, nif, nombre, apellido1, apellido2 FROM empleado WHERE apellido2 IN ('Díaz', 'Moreno');

+-------------+-----------+--------+-----------+-----------+
| id_empleado | nif       | nombre | apellido1 | apellido2 |
+-------------+-----------+--------+-----------+-----------+
|           2 | Y5575632D | Adela  | Salas     | Díaz      |
|           6 | 38382980M | María  | Santana   | Moreno    |
+-------------+-----------+--------+-----------+-----------+
2 rows in set (0,00 sec)
```

 35. Lista los nombres, apellidos y nif de los empleados que trabajan en el departamento 3.
```sql
SELECT nombre, apellido1, apellido2, nif FROM empleado WHERE id_departamento = 3;

+--------+-----------+-----------+-----------+
| nombre | apellido1 | apellido2 | nif       |
+--------+-----------+-----------+-----------+
| Adolfo | Rubio     | Flores    | R6970642B |
| Pepe   | Ruiz      | Santana   | 71651431Z |
+--------+-----------+-----------+-----------+
2 rows in set (0,00 sec)
```

 36. Lista los nombres, apellidos y nif de los empleados que trabajan en los departamentos 2, 4 o 5.
```sql
SELECT nombre, apellido1, apellido2, nif FROM empleado WHERE id_departamento IN (2, 4, 5);

+---------+-----------+-----------+-----------+
| nombre  | apellido1 | apellido2 | nif       |
+---------+-----------+-----------+-----------+
| Adela   | Salas     | Díaz      | Y5575632D |
| Pilar   | Ruiz      | NULL      | 80576669X |
| Juan    | Gómez     | López     | 56399183D |
| Adrián  | Suárez    | NULL      | 77705545E |
| Marcos  | Loyola    | Méndez    | 17087203C |
| Diego   | Flores    | Salas     | 46384486H |
+---------+-----------+-----------+-----------+
6 rows in set (0,00 sec)
```

## Consultas multitabla (Composición interna)

 1. Devuelve un listado con los empleados y los datos de los departamentos donde trabaja cada uno.
```sql
SELECT e.id_empleado, e.nif, e.nombre, e.apellido1, e.apellido2, d.id_departamento, d.nombre AS nombre_departamento, d.presupuesto, d.gastos 
FROM empleado e
INNER JOIN departamento d ON e.id_departamento = d.id_departamento;
```

```
+-------------+-----------+---------+-----------+-----------+-----------------+---------------------+-------------+--------+
| id_empleado | nif       | nombre  | apellido1 | apellido2 | id_departamento | nombre_departamento | presupuesto | gastos |
+-------------+-----------+---------+-----------+-----------+-----------------+---------------------+-------------+--------+
|           1 | 32481596F | Aarón   | Rivero    | Gómez     |               1 | Desarrollo          |      120000 |   6000 |
|           2 | Y5575632D | Adela   | Salas     | Díaz      |               2 | Sistemas            |      150000 |  21000 |
|           3 | R6970642B | Adolfo  | Rubio     | Flores    |               3 | Recursos Humanos    |      280000 |  25000 |
|           4 | 77705545E | Adrián  | Suárez    | NULL      |               4 | Contabilidad        |      110000 |   3000 |
|           5 | 17087203C | Marcos  | Loyola    | Méndez    |               5 | I+D                 |      375000 | 380000 |
|           6 | 38382980M | María   | Santana   | Moreno    |               1 | Desarrollo          |      120000 |   6000 |
|           7 | 80576669X | Pilar   | Ruiz      | NULL      |               2 | Sistemas            |      150000 |  21000 |
|           8 | 71651431Z | Pepe    | Ruiz      | Santana   |               3 | Recursos Humanos    |      280000 |  25000 |
|           9 | 56399183D | Juan    | Gómez     | López     |               2 | Sistemas            |      150000 |  21000 |
|          10 | 46384486H | Diego   | Flores    | Salas     |               5 | I+D                 |      375000 | 380000 |
|          11 | 67389283A | Marta   | Herrera   | Gil       |               1 | Desarrollo          |      120000 |   6000 |
+-------------+-----------+---------+-----------+-----------+-----------------+---------------------+-------------+--------+
11 rows in set (0,01 sec)
```



  2. Devuelve un listado con los empleados y los datos de los departamentos donde trabaja cada uno. Ordena el resultado, en primer lugar por el nombre del departamento (en orden alfabético) y en segundo lugar por los apellidos y el nombre de los empleados.

```sql
SELECT e.id_empleado, e.nif, e.nombre, e.apellido1, e.apellido2, d.id_departamento, d.nombre AS nombre_departamento, d.presupuesto, d.gastos
FROM empleado e
INNER JOIN departamento d ON e.id_departamento = d.id_departamento
ORDER BY d.nombre, e.apellido1, e.nombre;

+-------------+-----------+---------+-----------+-----------+-----------------+---------------------+-------------+--------+
| id_empleado | nif       | nombre  | apellido1 | apellido2 | id_departamento | nombre_departamento | presupuesto | gastos |
+-------------+-----------+---------+-----------+-----------+-----------------+---------------------+-------------+--------+
|           4 | 77705545E | Adrián  | Suárez    | NULL      |               4 | Contabilidad        |      110000 |   3000 |
|          11 | 67389283A | Marta   | Herrera   | Gil       |               1 | Desarrollo          |      120000 |   6000 |
|           1 | 32481596F | Aarón   | Rivero    | Gómez     |               1 | Desarrollo          |      120000 |   6000 |
|           6 | 38382980M | María   | Santana   | Moreno    |               1 | Desarrollo          |      120000 |   6000 |
|          10 | 46384486H | Diego   | Flores    | Salas     |               5 | I+D                 |      375000 | 380000 |
|           5 | 17087203C | Marcos  | Loyola    | Méndez    |               5 | I+D                 |      375000 | 380000 |
|           3 | R6970642B | Adolfo  | Rubio     | Flores    |               3 | Recursos Humanos    |      280000 |  25000 |
|           8 | 71651431Z | Pepe    | Ruiz      | Santana   |               3 | Recursos Humanos    |      280000 |  25000 |
|           9 | 56399183D | Juan    | Gómez     | López     |               2 | Sistemas            |      150000 |  21000 |
|           7 | 80576669X | Pilar   | Ruiz      | NULL      |               2 | Sistemas            |      150000 |  21000 |
|           2 | Y5575632D | Adela   | Salas     | Díaz      |               2 | Sistemas            |      150000 |  21000 |
+-------------+-----------+---------+-----------+-----------+-----------------+---------------------+-------------+--------+
11 rows in set (0,00 sec)
```

 3. Devuelve un listado con el identificador y el nombre del departamento, solamente de aquellos departamentos que tienen empleados.
```sql
SELECT d.id_departamento, d.nombre
FROM departamento d
INNER JOIN empleado e ON d.id_departamento = e.id_departamento
GROUP BY d.id_departamento, d.nombre;

+-----------------+------------------+
| id_departamento | nombre           |
+-----------------+------------------+
|               1 | Desarrollo       |
|               2 | Sistemas         |
|               3 | Recursos Humanos |
|               4 | Contabilidad     |
|               5 | I+D              |
+-----------------+------------------+
5 rows in set (0,01 sec)
```

 4. Devuelve un listado con el identificador, el nombre del departamento y el valor del presupuesto actual del que dispone, solamente de aquellos departamentos que tienen empleados. El valor del presupuesto actual lo puede calcular restando al valor del presupuesto inicial (columna presupuesto) el valor de los gastos que ha generado (columna gastos).
```sql
SELECT d.id_departamento, d.nombre, (d.presupuesto - d.gastos) AS presupuesto_actual 
FROM departamento d
INNER JOIN empleado e ON d.id_departamento = e.id_departamento;

+-----------------+------------------+--------------------+
| id_departamento | nombre           | presupuesto_actual |
+-----------------+------------------+--------------------+
|               1 | Desarrollo       |             114000 |
|               1 | Desarrollo       |             114000 |
|               1 | Desarrollo       |             114000 |
|               2 | Sistemas         |             129000 |
|               2 | Sistemas         |             129000 |
|               2 | Sistemas         |             129000 |
|               3 | Recursos Humanos |             255000 |
|               3 | Recursos Humanos |             255000 |
|               4 | Contabilidad     |             107000 |
|               5 | I+D              |              -5000 |
|               5 | I+D              |              -5000 |
+-----------------+------------------+--------------------+
11 rows in set (0,00 sec)
```

 5. Devuelve el nombre del departamento donde trabaja el empleado que tiene el nif '38382980M'.
```sql
SELECT d.nombre
FROM departamento d
INNER JOIN empleado e ON d.id_departamento = e.id_departamento
WHERE e.nif = '38382980M';

+------------+
| nombre     |
+------------+
| Desarrollo |
+------------+
1 row in set (	0,00 sec)
```

 6. Devuelve el nombre del departamento donde trabaja el empleado 'Pepe Ruiz Santana'.
```sql
SELECT d.nombre
FROM departamento d
INNER JOIN empleado e ON d.id_departamento = e.id_departamento
WHERE e.nombre = 'Pepe' AND e.apellido1 = 'Ruiz' AND e.apellido2 = 'Santana';

+------------------+
| nombre           |
+------------------+
| Recursos Humanos |
+------------------+
1 row in set (0,00 sec)
```

 7. Devuelve un listado con los datos de los empleados que trabajan en el departamento de I+D. Ordena el resultado alfabéticamente.
```sql
SELECT e.id_empleado, e.nif, e.nombre, e.apellido1, e.apellido2 
FROM empleado e
INNER JOIN departamento d ON e.id_departamento = d.id_departamento
WHERE d.nombre = 'I+D'
ORDER BY e.nombre, e.apellido1, e.apellido2;

+-------------+-----------+--------+-----------+-----------+
| id_empleado | nif       | nombre | apellido1 | apellido2 |
+-------------+-----------+--------+-----------+-----------+
|          10 | 46384486H | Diego  | Flores    | Salas     |
|           5 | 17087203C | Marcos | Loyola    | Méndez    |
+-------------+-----------+--------+-----------+-----------+
2 rows in set (0,00 sec)
```

 8. Devuelve un listado con los datos de los empleados que trabajan en el departamento de Sistemas, Contabilidad o I+D. Ordena el resultado alfabéticamente.
```sql
SELECT e.id_empleado, e.nif, e.nombre, e.apellido1, e.apellido2
FROM empleado e
INNER JOIN departamento d ON e.id_departamento = d.id_departamento
WHERE d.nombre IN ('Sistemas', 'Contabilidad', 'I+D')
ORDER BY e.nombre, e.apellido1, e.apellido2;

+-------------+-----------+---------+-----------+-----------+
| id_empleado | nif       | nombre  | apellido1 | apellido2 |
+-------------+-----------+---------+-----------+-----------+
|           2 | Y5575632D | Adela   | Salas     | Díaz      |
|           4 | 77705545E | Adrián  | Suárez    | NULL      |
|          10 | 46384486H | Diego   | Flores    | Salas     |
|           9 | 56399183D | Juan    | Gómez     | López     |
|           5 | 17087203C | Marcos  | Loyola    | Méndez    |
|           7 | 80576669X | Pilar   | Ruiz      | NULL      |
+-------------+-----------+---------+-----------+-----------+
6 rows in set (0,00 sec)
```

 9. Devuelve una lista con el nombre de los empleados que tienen los departamentos que no tienen un presupuesto entre 100000 y 200000 euros.
```sql
SELECT e.nombre
FROM empleado e
INNER JOIN departamento d ON e.id_departamento = d.id_departamento
WHERE d.presupuesto NOT BETWEEN 100000 AND 200000;

+--------+
| nombre |
+--------+
| Adolfo |
| Marcos |
| Pepe   |
| Diego  |
+--------+
4 rows in set (0,00 sec)
```

 10. Devuelve un listado con el nombre de los departamentos donde existe algún empleado cuyo segundo apellido sea NULL. Tenga en cuenta que no debe mostrar nombres de departamentos que estén repetidos.	
```sql
SELECT DISTINCT d.nombre
FROM departamento d
INNER JOIN empleado e ON d.id_departamento = e.id_departamento
WHERE e.apellido2 IS NULL;

+--------------+
| nombre       |
+--------------+
| Contabilidad |
| Sistemas     |
+--------------+
2 rows in set (0,00 sec)
```

## Consultas multitabla (Composición externa)

 1. Devuelve un listado con todos los empleados junto con los datos de los departamentos donde trabajan. Este listado también debe incluir los empleados que no tienen ningún departamento asociado.
```sql
SELECT e.id_empleado, e.nif, e.nombre, e.apellido1, e.apellido2, d.id_departamento, d.nombre AS nombre_departamento, d.presupuesto, d.gastos
FROM empleado e
LEFT JOIN departamento d ON e.id_departamento = d.id_departamento;

+-------------+-----------+--------------+-----------+-----------+-----------------+---------------------+-------------+--------+
| id_empleado | nif       | nombre       | apellido1 | apellido2 | id_departamento | nombre_departamento | presupuesto | gastos |
+-------------+-----------+--------------+-----------+-----------+-----------------+---------------------+-------------+--------+
|           1 | 32481596F | Aarón        | Rivero    | Gómez     |               1 | Desarrollo          |      120000 |   6000 |
|           2 | Y5575632D | Adela        | Salas     | Díaz      |               2 | Sistemas            |      150000 |  21000 |
|           3 | R6970642B | Adolfo       | Rubio     | Flores    |               3 | Recursos Humanos    |      280000 |  25000 |
|           4 | 77705545E | Adrián       | Suárez    | NULL      |               4 | Contabilidad        |      110000 |   3000 |
|           5 | 17087203C | Marcos       | Loyola    | Méndez    |               5 | I+D                 |      375000 | 380000 |
|           6 | 38382980M | María        | Santana   | Moreno    |               1 | Desarrollo          |      120000 |   6000 |
|           7 | 80576669X | Pilar        | Ruiz      | NULL      |               2 | Sistemas            |      150000 |  21000 |
|           8 | 71651431Z | Pepe         | Ruiz      | Santana   |               3 | Recursos Humanos    |      280000 |  25000 |
|           9 | 56399183D | Juan         | Gómez     | López     |               2 | Sistemas            |      150000 |  21000 |
|          10 | 46384486H | Diego        | Flores    | Salas     |               5 | I+D                 |      375000 | 380000 |
|          11 | 67389283A | Marta        | Herrera   | Gil       |               1 | Desarrollo          |      120000 |   6000 |
|          12 | 41234836R | Irene        | Salas     | Flores    |            NULL | NULL                |        NULL |   NULL |
|          13 | 82635162B | Juan Antonio | Sáez      | Guerrero  |            NULL | NULL                |        NULL |   NULL |
+-------------+-----------+--------------+-----------+-----------+-----------------+---------------------+-------------+--------+
13 rows in set (0,00 sec)
```

 2. Devuelve un listado donde sólo aparezcan aquellos empleados que no tienen ningún departamento asociado.
```sql
SELECT e.id_empleado, e.nif, e.nombre, e.apellido1, e.apellido2
FROM empleado e
LEFT JOIN departamento d ON e.id_departamento = d.id_departamento
WHERE d.id_departamento IS NULL;

+-------------+-----------+--------------+-----------+-----------+
| id_empleado | nif       | nombre       | apellido1 | apellido2 |
+-------------+-----------+--------------+-----------+-----------+
|          12 | 41234836R | Irene        | Salas     | Flores    |
|          13 | 82635162B | Juan Antonio | Sáez      | Guerrero  |
+-------------+-----------+--------------+-----------+-----------+
2 rows in set (0,00 sec)
```

 3. Devuelve un listado donde sólo aparezcan aquellos departamentos que no tienen ningún empleado asociado.
```sql
SELECT d.id_departamento, d.nombre, d.presupuesto, d.gastos
FROM departamento d
LEFT JOIN empleado e ON d.id_departamento = e.id_departamento
WHERE e.id_empleado IS NULL;

+-----------------+------------+-------------+--------+
| id_departamento | nombre     | presupuesto | gastos |
+-----------------+------------+-------------+--------+
|               6 | Proyectos  |           0 |      0 |
|               7 | Publicidad |           0 |   1000 |
+-----------------+------------+-------------+--------+
2 rows in set (0,00 sec)
```

 4. Devuelve un listado con todos los empleados junto con los datos de los departamentos donde trabajan. El listado debe incluir los empleados que no tienen ningún departamento asociado y los departamentos que no tienen ningún empleado asociado. Ordene el listado alfabéticamente por el nombre del departamento.
```sql
SELECT e.id_empleado, e.nif, e.nombre, e.apellido1, e.apellido2, d.id_departamento, d.nombre AS nombre_departamento, d.presupuesto, d.gastos
FROM empleado e
LEFT JOIN departamento d ON e.id_departamento = d.id_departamento
ORDER BY d.nombre;
+-------------+-----------+--------------+-----------+-----------+-----------------+---------------------+-------------+--------+
| id_empleado | nif       | nombre       | apellido1 | apellido2 | id_departamento | nombre_departamento | presupuesto | gastos |
+-------------+-----------+--------------+-----------+-----------+-----------------+---------------------+-------------+--------+
|          12 | 41234836R | Irene        | Salas     | Flores    |            NULL | NULL                |        NULL |   NULL |
|          13 | 82635162B | Juan Antonio | Sáez      | Guerrero  |            NULL | NULL                |        NULL |   NULL |
|           4 | 77705545E | Adrián       | Suárez    | NULL      |               4 | Contabilidad        |      110000 |   3000 |
|           1 | 32481596F | Aarón        | Rivero    | Gómez     |               1 | Desarrollo          |      120000 |   6000 |
|           6 | 38382980M | María        | Santana   | Moreno    |               1 | Desarrollo          |      120000 |   6000 |
|          11 | 67389283A | Marta        | Herrera   | Gil       |               1 | Desarrollo          |      120000 |   6000 |
|           5 | 17087203C | Marcos       | Loyola    | Méndez    |               5 | I+D                 |      375000 | 380000 |
|          10 | 46384486H | Diego        | Flores    | Salas     |               5 | I+D                 |      375000 | 380000 |
|           3 | R6970642B | Adolfo       | Rubio     | Flores    |               3 | Recursos Humanos    |      280000 |  25000 |
|           8 | 71651431Z | Pepe         | Ruiz      | Santana   |               3 | Recursos Humanos    |      280000 |  25000 |
|           2 | Y5575632D | Adela        | Salas     | Díaz      |               2 | Sistemas            |      150000 |  21000 |
|           7 | 80576669X | Pilar        | Ruiz      | NULL      |               2 | Sistemas            |      150000 |  21000 |
|           9 | 56399183D | Juan         | Gómez     | López     |               2 | Sistemas            |      150000 |  21000 |
+-------------+-----------+--------------+-----------+-----------+-----------------+---------------------+-------------+--------+
13 rows in set (0,00 sec)
```

 5. Devuelve un listado con los empleados que no tienen ningún departamento asociado y los departamentos que no tienen ningún empleado asociado. Ordene el listado alfabéticamente por el nombre del departamento.
```sql
SELECT
    COALESCE(e.id_empleado, 0) AS id_empleado,
    COALESCE(e.nif, '') AS nif,
    COALESCE(e.nombre, '') AS nombre,
    COALESCE(e.apellido1, '') AS apellido1,
    COALESCE(e.apellido2, '') AS apellido2,
    COALESCE(d.id_departamento, 0) AS id_departamento,
    COALESCE(d.nombre, '') AS nombre_departamento,
    COALESCE(d.presupuesto, 0) AS presupuesto,
    COALESCE(d.gastos, 0) AS gastos
FROM
    empleado e
LEFT JOIN
    departamento d ON e.id_departamento = d.id_departamento
UNION
SELECT
    COALESCE(e.id_empleado, 0) AS id_empleado,
    COALESCE(e.nif, '') AS nif,
    COALESCE(e.nombre, '') AS nombre,
    COALESCE(e.apellido1, '') AS apellido1,
    COALESCE(e.apellido2, '') AS apellido2,
    COALESCE(d.id_departamento, 0) AS id_departamento,
    COALESCE(d.nombre, '') AS nombre_departamento,
    COALESCE(d.presupuesto, 0) AS presupuesto,
    COALESCE(d.gastos, 0) AS gastos
FROM
    empleado e
RIGHT JOIN
    departamento d ON e.id_departamento = d.id_departamento
ORDER BY
    nombre_departamento;
    
+-------------+-----------+--------------+-----------+-----------+-----------------+---------------------+-------------+--------+
| id_empleado | nif       | nombre       | apellido1 | apellido2 | id_departamento | nombre_departamento | presupuesto | gastos |
+-------------+-----------+--------------+-----------+-----------+-----------------+---------------------+-------------+--------+
|          12 | 41234836R | Irene        | Salas     | Flores    |               0 |                     |           0 |      0 |
|          13 | 82635162B | Juan Antonio | Sáez      | Guerrero  |               0 |                     |           0 |      0 |
|           4 | 77705545E | Adrián       | Suárez    |           |               4 | Contabilidad        |      110000 |   3000 |
|           1 | 32481596F | Aarón        | Rivero    | Gómez     |               1 | Desarrollo          |      120000 |   6000 |
|           6 | 38382980M | María        | Santana   | Moreno    |               1 | Desarrollo          |      120000 |   6000 |
|          11 | 67389283A | Marta        | Herrera   | Gil       |               1 | Desarrollo          |      120000 |   6000 |
|           5 | 17087203C | Marcos       | Loyola    | Méndez    |               5 | I+D                 |      375000 | 380000 |
|          10 | 46384486H | Diego        | Flores    | Salas     |               5 | I+D                 |      375000 | 380000 |
|           0 |           |              |           |           |               6 | Proyectos           |           0 |      0 |
|           0 |           |              |           |           |               7 | Publicidad          |           0 |   1000 |
|           3 | R6970642B | Adolfo       | Rubio     | Flores    |               3 | Recursos Humanos    |      280000 |  25000 |
|           8 | 71651431Z | Pepe         | Ruiz      | Santana   |               3 | Recursos Humanos    |      280000 |  25000 |
|           2 | Y5575632D | Adela        | Salas     | Díaz      |               2 | Sistemas            |      150000 |  21000 |
|           7 | 80576669X | Pilar        | Ruiz      |           |               2 | Sistemas            |      150000 |  21000 |
|           9 | 56399183D | Juan         | Gómez     | López     |               2 | Sistemas            |      150000 |  21000 |
+-------------+-----------+--------------+-----------+-----------+-----------------+---------------------+-------------+--------+
15 rows in set (0,00 sec)
```

## Consultas resumen

 1. Calcula la suma del presupuesto de todos los departamentos.
```sql
SELECT SUM(d.presupuesto) AS total_presupuesto 
FROM departamento d;

+-------------------+
| total_presupuesto |
+-------------------+
|           1035000 |
+-------------------+
1 row in set (0,01 sec)
```

 2. Calcula la media del presupuesto de todos los departamentos.
```sql
SELECT AVG(d.presupuesto) AS media_presupuesto
FROM departamento d;
+-------------------+
| media_presupuesto |
+-------------------+
|       147857.1429 |
+-------------------+
1 row in set (0,00 sec)
```

 3. Calcula el valor mínimo del presupuesto de todos los departamentos.
```sql
SELECT MIN(d.presupuesto) AS min_presupuesto
FROM departamento d;
+-----------------+
| min_presupuesto |
+-----------------+
|               0 |
+-----------------+
1 row in set (0,00 sec)
```

 4. Calcula el nombre del departamento y el presupuesto que tiene asignado, del departamento con menor presupuesto.
```sql
SELECT d.nombre, d.presupuesto
FROM departamento d
ORDER BY d.presupuesto ASC
LIMIT 1;
+-----------+-------------+
| nombre    | presupuesto |
+-----------+-------------+
| Proyectos |           0 |
+-----------+-------------+
1 row in set (0,00 sec)
```

 5. Calcula el valor máximo del presupuesto de todos los departamentos.
```sql
SELECT MAX(d.presupuesto) AS max_presupuesto
FROM departamento d;
+-----------------+
| max_presupuesto |
+-----------------+
|          375000 |
+-----------------+
1 row in set (0,00 sec)
```

 6. Calcula el nombre del departamento y el presupuesto que tiene asignado, del departamento con mayor presupuesto.
```sql
SELECT d.nombre, d.presupuesto
FROM departamento d
ORDER BY d.presupuesto DESC
LIMIT 1;
+--------+-------------+
| nombre | presupuesto |
+--------+-------------+
| I+D    |      375000 |
+--------+-------------+
1 row in set (0,00 sec)
```

 7. Calcula el número total de empleados que hay en la tabla empleado.
```sql
SELECT COUNT(*) AS total_empleados
FROM empleado;
+-----------------+
| total_empleados |
+-----------------+
|              13 |
+-----------------+
1 row in set (0,01 sec)
```

 8. Calcula el número de empleados que no tienen NULL en su segundo apellido.
```sql
SELECT COUNT(*) AS empleados_con_segundo_apellido
FROM empleado
WHERE apellido2 IS NOT NULL;
+--------------------------------+
| empleados_con_segundo_apellido |
+--------------------------------+
|                             11 |
+--------------------------------+
1 row in set (0,00 sec)
```

 9. Calcula el número de empleados que hay en cada departamento. Tienes que devolver dos columnas, una con el nombre del departamento y otra con el número de empleados que tiene asignados.
```sql
SELECT d.nombre, COUNT(*) AS num_empleados
FROM departamento d
LEFT JOIN empleado e ON d.id_departamento = e.id_departamento
GROUP BY d.nombre;
+------------------+---------------+
| nombre           | num_empleados |
+------------------+---------------+
| Desarrollo       |             3 |
| Sistemas         |             3 |
| Recursos Humanos |             2 |
| Contabilidad     |             1 |
| I+D              |             2 |
| Proyectos        |             1 |
| Publicidad       |             1 |
+------------------+---------------+
7 rows in set (0,00 sec)
```

 10. Calcula el nombre de los departamentos que tienen más de 2 empleados. El resultado debe tener dos columnas, una con el nombre del departamento y otra con el número de empleados que tiene asignados.
```sql
SELECT d.nombre, COUNT(*) AS num_empleados
FROM departamento d
INNER JOIN empleado e ON d.id_departamento = e.id_departamento
GROUP BY d.nombre
HAVING COUNT(*) > 2;
+------------+---------------+
| nombre     | num_empleados |
+------------+---------------+
| Desarrollo |             3 |
| Sistemas   |             3 |
+------------+---------------+
2 rows in set (0,00 sec)
```

 11. Calcula el número de empleados que trabajan en cada uno de los departamentos. El resultado de esta consulta también tiene que incluir aquellos departamentos que no tienen ningún empleado asociado.
```sql
SELECT d.nombre, COALESCE(COUNT(*), 0) AS num_empleados
FROM departamento d
LEFT JOIN empleado e ON d.id_departamento = e.id_departamento
GROUP BY d.nombre;
+------------------+---------------+
| nombre           | num_empleados |
+------------------+---------------+
| Desarrollo       |             3 |
| Sistemas         |             3 |
| Recursos Humanos |             2 |
| Contabilidad     |             1 |
| I+D              |             2 |
| Proyectos        |             1 |
| Publicidad       |             1 |
+------------------+---------------+
7 rows in set (0,00 sec)
```

 12. Calcula el número de empleados que trabajan en cada unos de los departamentos que tienen un presupuesto mayor a 200000 euros.
```sql
SELECT d.nombre, COUNT(*) AS num_empleados
FROM departamento d
INNER JOIN empleado e ON d.id_departamento = e.id_departamento
WHERE d.presupuesto > 200000
GROUP BY d.nombre;

+------------------+---------------+
| nombre           | num_empleados |
+------------------+---------------+
| Recursos Humanos |             2 |
| I+D              |             2 |
+------------------+---------------+
2 rows in set (0,00 sec)
```

## Subconsultas

 Con operadores básicos de comparación

 1. Devuelve un listado con todos los empleados que tiene el departamento de Sistemas. (Sin utilizar INNER JOIN).
```sql
SELECT id_empleado, nif, nombre, apellido1, apellido2
FROM empleado
WHERE id_departamento = (SELECT id_departamento FROM departamento WHERE nombre = 'Sistemas');

+-------------+-----------+--------+-----------+-----------+
| id_empleado | nif       | nombre | apellido1 | apellido2 |
+-------------+-----------+--------+-----------+-----------+
|           2 | Y5575632D | Adela  | Salas     | Díaz      |
|           7 | 80576669X | Pilar  | Ruiz      | NULL      |
|           9 | 56399183D | Juan   | Gómez     | López     |
+-------------+-----------+--------+-----------+-----------+
3 rows in set (0,00 sec)
```

 2. Devuelve el nombre del departamento con mayor presupuesto y la cantidad que tiene asignada.
```sql
SELECT d.nombre, d.presupuesto
FROM departamento d
WHERE d.presupuesto = (SELECT MAX(presupuesto) FROM departamento);
+--------+-------------+
| nombre | presupuesto |
+--------+-------------+
| I+D    |      375000 |
+--------+-------------+
1 row in set (0,00 sec)
```

 3. Devuelve el nombre del departamento con menor presupuesto y la cantidad que tiene asignada.
```sql
SELECT d.nombre, d.presupuesto
FROM departamento d
WHERE d.presupuesto = (SELECT MIN(presupuesto) FROM departamento);
+------------+-------------+
| nombre     | presupuesto |
+------------+-------------+
| Proyectos  |           0 |
| Publicidad |           0 |
+------------+-------------+
2 rows in set (0,01 sec)
```

#####  Subconsultas con ALL y ANY

 4. Devuelve el nombre del departamento con mayor presupuesto y la cantidad que tiene asignada. Sin hacer uso de MAX, ORDER BY ni LIMIT.
```sql
SELECT d.nombre, d.presupuesto
FROM departamento d
WHERE d.presupuesto >= ALL (SELECT presupuesto FROM departamento);
+--------+-------------+
| nombre | presupuesto |
+--------+-------------+
| I+D    |      375000 |
+--------+-------------+
1 row in set (0,00 sec)
```

 5. Devuelve el nombre del departamento con menor presupuesto y la cantidad que tiene asignada. Sin hacer uso de MIN, ORDER BY ni LIMIT.
```sql
SELECT d.nombre, d.presupuesto
FROM departamento d
WHERE d.presupuesto <= ALL (SELECT presupuesto FROM departamento);
+------------+-------------+
| nombre     | presupuesto |
+------------+-------------+
| Proyectos  |           0 |
| Publicidad |           0 |
+------------+-------------+
2 rows in set (0,00 sec)
```

 6. Devuelve los nombres de los departamentos que tienen empleados asociados. (Utilizando ALL o ANY).
```sql
SELECT d.nombre
FROM departamento d
WHERE EXISTS (SELECT 1 FROM empleado e WHERE e.id_departamento = d.id_departamento);
+------------------+
| nombre           |
+------------------+
| Desarrollo       |
| Sistemas         |
| Recursos Humanos |
| Contabilidad     |
| I+D              |
+------------------+
5 rows in set (0,00 sec)
```

 7. Devuelve los nombres de los departamentos que no tienen empleados asociados. (Utilizando ALL o ANY).
```sql
SELECT d.nombre 
FROM departamento d
WHERE NOT EXISTS (SELECT 1 FROM empleado e WHERE e.id_departamento = d.id_departamento);

+------------+
| nombre     |
+------------+
| Proyectos  |
| Publicidad |
+------------+
2 rows in set (0,00 sec)
```

#####  Subconsultas con IN y NOT IN

 8. Devuelve los nombres de los departamentos que tienen empleados asociados. (Utilizando IN o NOT IN).
```sql
SELECT d.nombre
FROM departamento d
WHERE d.id_departamento IN (SELECT id_departamento FROM empleado);
+------------------+
| nombre           |
+------------------+
| Desarrollo       |
| Sistemas         |
| Recursos Humanos |
| Contabilidad     |
| I+D              |
+------------------+
5 rows in set (0,01 sec)
```

 9. Devuelve los nombres de los departamentos que no tienen empleados asociados. (Utilizando IN o NOT IN).
```sql
SELECT d.nombre
FROM departamento d
LEFT JOIN empleado e ON d.id_departamento = e.id_departamento
WHERE e.id_empleado IS NULL;
+------------+
| nombre     |
+------------+
| Proyectos  |
| Publicidad |
+------------+
2 rows in set (0,00 sec)
```

#####  Subconsultas con EXISTS y NOT EXISTS

 10. Devuelve los nombres de los departamentos que tienen empleados asociados. (Utilizando EXISTS o NOT EXISTS).
```sql
SELECT d.nombre
FROM departamento d
WHERE EXISTS (SELECT 1 FROM empleado e WHERE e.id_departamento = d.id_departamento);
+------------------+
| nombre           |
+------------------+
| Desarrollo       |
| Sistemas         |
| Recursos Humanos |
| Contabilidad     |
| I+D              |
+------------------+
5 rows in set (0,00 sec)
```

 11. Devuelve los nombres de los departamentos que tienen empleados asociados. (Utilizando EXISTS o NOT EXISTS)
```sql
SELECT d.nombre
FROM departamento d
WHERE EXISTS (SELECT 1 FROM empleado e WHERE e.id_departamento = d.id_departamento);
+------------------+
| nombre           |
+------------------+
| Desarrollo       |
| Sistemas         |
| Recursos Humanos |
| Contabilidad     |
| I+D              |
+------------------+
5 rows in set (0,00 sec)
```