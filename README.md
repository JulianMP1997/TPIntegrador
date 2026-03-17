| Campo               | Descripción / Ejemplo                                                                                 |
| ------------------- | ----------------------------------------------------------------------------------------------------- |
| Nombre del Proyecto | Sistema de Búsqueda de Alquiler Permanente                                                            |
| MVP                 | Permitir a propietarios publicar propiedades y a clientes buscar alquileres según ubicación y precio  |
| Entidad 1           | Propietario (id, nombre, dirección, teléfono, propiedadesId, categoriaId)                             |
| Entidad 2           | Cliente (id, nombre, teléfono, propiedadesId)                                                         |
| Entidad 3           | Propiedades (id, nombre, descripción, precio, stock, categoriaId)                                     |
| Relación            | Un propietario tiene muchas propiedades; cada propiedad puede ser alquilada por un solo cliente (1:N) |
| Historia 1          | Como propietario, quiero publicar una propiedad para alquilar rápidamente                             |
| Historia 2          | Como cliente, quiero buscar una propiedad en Crespo para vivir y trabajar                             |
| Historia 3          | Como cliente, quiero buscar alquileres dentro de un rango de precio                                   |
| Historia 4          | Como propietario, quiero listar todas mis propiedades disponibles                                     |
| Historia 5          | Como propietario, quiero ordenar mis propiedades según tiempo publicadas                              |
