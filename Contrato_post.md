📋 Contrato del Endpoint - Crear Propiedad
Endpoint:
POST /api/propiedades
Descripción:
Crea una nueva propiedad en el sistema.

Request
Método: POST
Content-Type: application/json
Body (JSON):
JSON{
  "titulo": "Casa amplia con patio",
  "descripcion": "Hermosa casa familiar con jardín y cochera",
  "precio": 150000,
  "ubicacion": "Calle Falsa 123, Resistencia",
  "cantidad_ambientes": 4,
  "cantidad_dormitorios": 3,
  "cantidad_banos": 2,
  "capacidad": 5,
  "disponible": true,
  "categoria_id": 1
}

Response Exitosa
Código: 201 Created
JSON{
  "ok": true,
  "mensaje": "Propiedad creada correctamente",
  "data": {
    "id": 10,
    "titulo": "Casa amplia con patio",
    "precio": 150000,
    "disponible": true
  }
}

Response con Errores de Validación
Código: 400 Bad Request
JSON{
  "ok": false,
  "errores": {
    "titulo": "Campo obligatorio",
    "precio": "Debe ser mayor que 0",
    "ubicacion": "Debe contener entre 10 y 100 caracteres"
  }
}
