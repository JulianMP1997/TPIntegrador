01. FERNANDEZ MARIANO
PRETZ JULIAN
NAHUEL GEIST
GERMAN MEDRANO

SISTEMA DE BUSQUEDA DE ALQUILER PERMANENTE

02. Un sistema en el cual, por un lado un propietario pueda poner en alquiler de forma rapida y sencilla
su propiedad, y por tro lado, que el cliente pueda buscar alquiler en su localidad o en zonas aledañas, adaptandose
a sus necesidades.

03. Al principio definimos 3 entidades:
   , 
    A- Propietario. (id, nombre, dirección, telefono, PropiedadesId, CategoriaId).
    B- Cliente (id, nombre, telefono, PropiedadesId).
    C- Propiedades (id, nombre, descripción, precio, stock, categoriaId).

Un propietario puede tener muchas propiedades, cada propiedad puede ser alquilada por un solo cliente.

04. Estas son las 5 historias de usuario principales para nuestro sistema:
  
    A- Como propietario, quiero publicar una propiedad para vender.
    B- Como cliente, quiero buscar una propiedad en Crespo para vivir y poder trabajar en esa misma localidad.
    C- Como cliente, quiero buscar un alquiler dentro de un rango de precio para que se adecue a mi presupuesto.
    D- Como propietario, quiero listar todas las propiedades que tenga disponibles.
    E- Como propietario, quiero ordenar mis propiedades en base a cuanto llevan publicadas, que no se hayan alquilado.
    
