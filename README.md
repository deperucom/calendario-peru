# Calendario del Perú y el mundo — API de DePeru.com

Repositorio informativo sobre el calendario diario de eventos y celebraciones publicado por [DePeru.com](https://www.deperu.com) y su endpoint JSON. Documenta la estructura de respuesta observada y muestra ejemplos para consultar los eventos asociados a cada día.

> **Este repositorio es independiente y no está afiliado oficialmente a DePeru.com.** Los datos y el servicio son proporcionados por DePeru.com. Verifica la información en la fuente original antes de depender de ella.

## Enlaces

- **Calendario:** https://www.deperu.com/calendario/
- **Endpoint JSON:** https://deperu.com/api/rest/calendarioPeru.json
- **Contacto DePeru.com:** https://deperu.com/contacto

## ¿Qué ofrece el servicio?

El endpoint entrega una lista de eventos o celebraciones asociados al día consultado, tanto del Perú como internacionales. Cada elemento puede incluir un identificador, la fecha, el título, un resumen, una imagen y un enlace al detalle del evento.

### Características conocidas

| Propiedad | Detalle |
| --- | --- |
| Servicio | Calendario de eventos y celebraciones |
| Fuente | DePeru.com |
| Formato observado | JSON (arreglo de objetos) |
| Contenido | Eventos asociados al día en curso, según la descripción del servicio |
| Restricción geográfica | No especificada en la información disponible; verifica con el proveedor |
| Límite de solicitudes | No especificado en la información disponible |

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

La respuesta observada es un arreglo JSON. Los valores del ejemplo son ilustrativos y corresponden a la fecha indicada; la lista y los eventos pueden cambiar según el día y la actualización del servicio.

## Identifica tu aplicación con User-Agent

Se recomienda enviar un encabezado `User-Agent` que identifique el dominio o nombre de la aplicación cliente y su versión. Ejemplo:

```http
User-Agent: dePeru.info_Calendario/1.0
```

Reemplaza este valor por el identificador de tu propia aplicación o sitio.

## Consulta rápida

```bash
curl --fail --silent --show-error \
  --max-time 10 \
  --user-agent 'dePeru.info_Calendario/1.0' \
  https://deperu.com/api/rest/calendarioPeru.json
```

Para ejemplos con manejo de errores en PHP, Python, Node.js y Java, consulta la [guía técnica](docs/guia-tecnica.md).

## Recomendaciones de consumo

- Envía un `User-Agent` identificable y reemplaza el ejemplo por los datos de tu aplicación.
- Comprueba que la respuesta sea un arreglo y valida los campos antes de usarlos.
- Trata `id` y `fecha` como cadenas, tal como aparecen en el ejemplo.
- Maneja errores de red, respuestas HTTP no exitosas y JSON inválido.
- Evita consultas repetitivas innecesarias; la lista es diaria, así que considera usar caché durante el día.
- No asumas SLA ni disponibilidad garantizada.

## Uso responsable y atribución

Al mostrar los eventos, conserva una atribución visible a **DePeru.com** y enlaza a la página del evento o al calendario cuando corresponda. Revisa las condiciones del proveedor antes de redistribuir contenido, resúmenes o imágenes.

## Documentación

- [Guía técnica de uso: cURL, PHP, Python, Node.js y Java](docs/guia-tecnica.md)
- [Descripción del servicio y estructura de la respuesta](docs/servicio.md)
- [Restricciones y buenas prácticas](docs/limitaciones.md)

## Aviso

Este proyecto es informativo y se basa en la estructura observada del endpoint. La URL, la respuesta y las políticas del proveedor pueden cambiar sin previo aviso; confirma la información con DePeru.com antes de depender del servicio en producción.
