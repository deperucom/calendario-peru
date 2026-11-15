# Restricciones y buenas prácticas

## Acceso y límites

La información disponible para este repositorio no especifica restricciones geográficas ni un límite de solicitudes. Consulta las condiciones vigentes del proveedor y evita asumir disponibilidad o frecuencia garantizadas.

## Contenido y derechos

La respuesta puede incluir resúmenes editoriales, imágenes y enlaces. Antes de redistribuirlos o incorporarlos a un producto, revisa las condiciones aplicables y conserva la atribución a DePeru.com.

## Buenas prácticas

- Identifica la aplicación con el User-Agent `dePeru.info_Calendario/1.0` o uno propio que identifique tu sitio.
- No hagas polling rápido ni solicitudes en bucle.
- Valida la estructura del arreglo y los campos antes de mostrarlos.
- Escapa texto no confiable al presentarlo en HTML.
- Valida que las URLs usen esquemas esperados (`https`) antes de mostrar imágenes o enlaces.
- Usa caché cuando corresponda y maneja errores HTTP, de red y de análisis JSON.

## Aviso

Esta documentación es informativa y se basa en el ejemplo proporcionado. El contenido, formato, disponibilidad y políticas del endpoint pueden cambiar sin previo aviso. Confirma la información directamente con DePeru.com.
