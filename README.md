# Sistema de Búsqueda de Alquiler Permanente - API REST (MVP)

Proyecto para permitir a propietarios publicar propiedades en alquiler permanente y a clientes buscarlas por ubicación precio y otros filtros.

| Campo               | Descripción                                                                                           |
| ------------------- | ----------------------------------------------------------------------------------------------------- |
| Nombre del Proyecto | Sistema de Búsqueda de Alquiler Permanente                                                            |
| MVP                 | Permitir a propietarios publicar propiedades y a clientes buscar alquileres según ubicación y precio  |
| Entidad 1           | Propietario (id, nombre, dirección, teléfono, propiedadesId, categoriaId)                             |
| Entidad 2           | Cliente (id, nombre, teléfono, propiedadesId)                                                         |
| Entidad 3           | Propiedades (id, nombre, descripción, precio, stock, categoriaId)                                     |
| Relación            | Un propietario tiene muchas propiedades; cada propiedad puede ser alquilada por un solo cliente (1:N) |

| ID | Historia                                                                  |
| -- | ------------------------------------------------------------------------- |
| 1  | Como propietario, quiero publicar una propiedad para alquilar rápidamente |
| 2  | Como cliente, quiero buscar una propiedad en Crespo para vivir y trabajar |
| 3  | Como cliente, quiero buscar alquileres dentro de un rango de precio       |
| 4  | Como propietario, quiero listar todas mis propiedades disponibles         |
| 5  | Como propietario, quiero ordenar mis propiedades según tiempo publicadas  |


Endpoints de la API versión MVP

| # | Método | Endpoint                     | Descripción principal                                                        | Parámetros / Body                                           | Historia |
|---|--------|------------------------------|------------------------------------------------------------------------------|-------------------------------------------------------------|----------|
| 1 | GET    | /health                      | Verifica que la API esté activa y responde con estado básico                 | —                                                           | —        |
| 2 | DELETE | /api/propiedades/{id}        | Elimina una propiedad solo el propietario autenticado                        | id en path                                                  | 4        |
| 3 | PUT    | /api/propiedades/{id}        | Actualiza datos de una propiedad precio descripción disponibilidad etc       | Body JSON + id en path                                      | 4 5      |
| 4 | POST   | /api/propiedades             | Crea y publica una nueva propiedad para alquilar                             | Body JSON                                                   | 1        |
| 5 | GET    | /api/propiedades             | Busca y lista propiedades con filtros ubicación precio categoría etc         | Query params todos opcionales                               | 2 3      |

Detalle completo de cada endpoint

1 Health Check  
GET /health  

Respuesta esperada 200 OK  
{  
  "status": "ok",  
  "timestamp": "2026-03-22T20:15:00-03:00",  
  "version": "0.1.0-mvp",  
  "environment": "development"  
}

2 Eliminar propiedad  
DELETE /api/propiedades/38492  

Respuestas  
204 No Content → Eliminada correctamente  
401 Unauthorized → No autenticado  
403 Forbidden → No es el propietario  
404 Not Found → Propiedad no existe

3 Actualizar propiedad  
PUT /api/propiedades/38492  
Content-Type: application/json  

{  
  "nombre": "Casa en barrio centro",  
  "descripcion": "3 dormitorios cocina ampliada 2025",  
  "precio": 180000,  
  "direccion": "San Martín 123 Crespo",  
  "categoriaId": 2,  
  "disponible": true  
}  

Respuestas  
200 OK → {propiedad actualizada}  
400 Bad Request → Datos inválidos  
401/403 → Autenticación / autorización  
404 Not Found

4 Publicar nueva propiedad  
POST /api/propiedades  
Content-Type: application/json  

{  
  "nombre": "Departamento Mitre 450",  
  "descripcion": "2 ambientes 1 baño balcón al fondo",  
  "precio": 150000,  
  "direccion": "Bv. Mitre 450 Crespo Entre Ríos",  
  "categoriaId": 1,  
  "disponible": true  
}  

Respuestas  
201 Created → { "id": 38492 ...propiedad completa... }  
400 Bad Request  
401 Unauthorized

5 Búsqueda / Listado de propiedades  
GET /api/propiedades?ubicacion=Crespo&precioMin=80000&precioMax=220000&categoria=1&orden=mas_reciente&pagina=1&limite=12  

Ejemplos  
GET /api/propiedades?ubicacion=Crespo  
GET /api/propiedades?precioMax=150000&disponible=true  
GET /api/propiedades?orden=precio_asc&limite=20  

Query parameters todos opcionales  

| Parámetro    | Tipo     | Descripción                                  | Ejemplo             | Default       |  
|--------------|----------|----------------------------------------------|---------------------|---------------|  
| ubicacion    | string   | Ciudad barrio o texto libre                  | Crespo              | —             |  
| precioMin    | number   | Precio mensual mínimo                        | 80000               | 0             |  
| precioMax    | number   | Precio mensual máximo                        | 250000              | ∞             |  
| categoria    | number   | ID categoría 1=depto 2=casa etc              | 1                   | —             |  
| disponible   | boolean  | Solo propiedades disponibles                 | true                | true          |  
| orden        | string   | mas_reciente precio_asc precio_desc          | mas_reciente        | mas_reciente  |  
| pagina       | integer  | Página de resultados                         | 1                   | 1             |  
| limite       | integer  | Resultados por página                        | 12                  | 12            |  

Respuesta ejemplo 200 OK  
{  
  "total": 47,  
  "pagina": 1,  
  "limite": 12,  
  "totalPaginas": 4,  
  "resultados": [  
    {  
      "id": 38492,  
      "nombre": "Departamento Mitre 450",  
      "descripcion": "2 ambientes 1 baño balcón",  
      "precio": 150000,  
      "direccion": "Bv. Mitre 450 Crespo",  
      "categoriaId": 1,  
      "publicadoEn": "2026-03-10T14:30:00-03:00",  
      "propietario": {  
        "id": 123,  
        "nombre": "Juan Pérez"  
      },  
      "disponible": true  
    }  
  ]  
}
