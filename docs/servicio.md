# Descripción del servicio

## Resumen

El endpoint de calendario de DePeru.com devuelve los eventos o celebraciones asociados al día. La respuesta de ejemplo es un arreglo de objetos, cada uno con información de identificación, fecha, título, resumen, imagen y URL de detalle.

## Enlaces

- Calendario: https://www.deperu.com/calendario/
- Endpoint: https://deperu.com/api/rest/calendarioPeru.json
- Contacto: https://deperu.com/contacto

## Ejemplo de respuesta

```json
[
  {
    "id": "2528",
    "fecha": "14 de noviembre",
    "titulo": "Día del Bibliotecario Peruano",
    "resumen": "Fecha que reconoce la destacada labor de los profesionales en bibliotecología, quienes preservan, gestionan y difunden nuestro patrimonio bibliográfico documental en el territorio nacional.",
    "imagen": "https://imgs.deperu.com/thumbnails/pasadizo_biblioteca.jpg",
    "url": "https://www.deperu.com/calendario/2528/dia-del-bibliotecario-peruano"
  },
  {
    "id": "1021",
    "fecha": "14 de noviembre",
    "titulo": "Día Mundial de la Diabetes",
    "resumen": "La diabetes es una enfermedad que no distingue sexo ni edad. Con el correr de los años se ha ido convirtiendo en uno de los males más peligrosos de la humanidad junto con el cáncer. Por ello, cada 14 de noviembre se toma consciencia sobre sus daños y se dan pasos importantes para su prevención.",
    "imagen": "https://imgs.deperu.com/thumbnails/diabetes_inyeccion.jpg",
    "url": "https://www.deperu.com/calendario/1021/dia-mundial-de-la-diabetes"
  },
  {
    "id": "2708",
    "fecha": "14 de noviembre",
    "titulo": "Semana Internacional de la Ciencia y la Paz",
    "resumen": "La celebración de esta semana subraya el compromiso de la comunidad científica y de la sociedad en general para utilizar el conocimiento en favor de la paz, promoviendo un desarrollo global equitativo y sostenible.",
    "imagen": "https://imgs.deperu.com/thumbnails/mujer_ciencia.jpg",
    "url": "https://www.deperu.com/calendario/2708/semana-internacional-de-la-ciencia-y-la-paz"
  },
  {
    "id": "2712",
    "fecha": "14 de noviembre",
    "titulo": "Semana de la Conservación y Manejo de la Vida Animal",
    "resumen": "Semana instituida para hacer frente a factores que impactan negativamente sobre la fauna silvestre, tales como la extracción selectiva con fines comerciales o deportivos, el cambio climático o la introducción de especies exóticas.",
    "imagen": "https://imgs.deperu.com/thumbnails/ronsocos.jpg",
    "url": "https://www.deperu.com/calendario/2712/semana-de-la-conservacion-y-manejo-de-la-vida-animal"
  }
]
```

## Estructura observada

| Campo | Tipo observado | Descripción |
| --- | --- | --- |
| `id` | Cadena | Identificador del evento |
| `fecha` | Cadena | Fecha legible, por ejemplo `14 de noviembre` |
| `titulo` | Cadena | Nombre del evento o celebración |
| `resumen` | Cadena | Descripción breve o informativa |
| `imagen` | Cadena (URL) | Imagen asociada al evento |
| `url` | Cadena (URL) | Enlace a la página de detalle |

## Consideraciones

- Los tipos y campos se describen a partir de la respuesta de ejemplo; valida el contenido recibido.
- La lista puede contener cero, uno o varios eventos según el día.
- El endpoint se describe como calendario del día en curso; la fecha de ejemplo no determina el contenido de otras fechas.
- Los textos e imágenes pueden tener condiciones de uso propias. Consulta al proveedor antes de redistribuirlos.
