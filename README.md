1. ¿Cuántas filas devuelve cada consulta y por qué son distintas?

UNION devuelve 11 filas y UNION ALL devuelve 14 filas.
La diferencia es que UNION elimina las filas completamente duplicadas, mientras que UNION ALL conserva todos los registros, incluso si se repiten.
En este caso, los productos repetidos en ambas sucursales son:

103 – Monitor 4K 27" – Computación
104 – Teclado Mecánico – Accesorios
106 – SSD Externo 1TB – Almacenamiento

Como estos tres registros tienen el mismo id_producto, nombre_producto y categoria, UNION los muestra una sola vez. Por eso elimina 3 filas y el resultado pasa de 14 a 11.
La Webcam HD 1080p no se elimina, aunque tenga el mismo nombre y categoría, porque su id_producto es diferente: 107 en Norte y 111 en Sur.


2. ¿Por qué UNION ALL es más eficiente que UNION?

UNION ALL es más eficiente porque únicamente combina los resultados de ambas consultas.
En cambio, UNION debe realizar una operación adicional para identificar y eliminar duplicados. Internamente, el motor puede ordenar o comparar las filas, lo que requiere mayor uso de memoria y procesamiento.
Por eso, cuando no es necesario eliminar registros repetidos, conviene usar UNION ALL.


3. ¿En qué casos de negocio usarías cada uno?

Usaría UNION cuando necesito obtener registros únicos. Por ejemplo:
- Consolidar una base de clientes de tienda física y tienda online sin repetir personas.
- Unificar catálogos de proveedores de distintas áreas evitando duplicados.

Usaría UNION ALL cuando cada fila representa un movimiento independiente y no se debe eliminar ninguna. Por ejemplo:
- Consolidar ventas de distintos meses.
- Unir movimientos de inventario de varios almacenes.


4. ¿Qué pasa si las columnas no coinciden en número o tipo?

Ambas consultas deben devolver la misma cantidad de columnas, en el mismo orden, y con tipos de datos compatibles.
Si una consulta devuelve cuatro columnas y la otra tres, SQL Server genera un error indicando que las consultas combinadas con UNION deben tener el mismo número de expresiones.

También puede generarse un error de conversión si los tipos de datos no son compatibles. Por ejemplo, si una columna es INT y la otra contiene texto que no puede convertirse a número.

Además, SQL combina las columnas por posición, no por nombre.
