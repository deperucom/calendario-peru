# Guía técnica de uso

Esta guía muestra cómo consultar el endpoint del calendario desde una aplicación:

```text
https://deperu.com/api/rest/calendarioPeru.json
```

La respuesta observada es un arreglo JSON de eventos o celebraciones asociados al día. Los ejemplos incluyen timeout, manejo básico de errores y el User-Agent recomendado.

## User-Agent personalizado

Se recomienda enviar un encabezado `User-Agent` que identifique el dominio o nombre de la aplicación cliente y su versión:

```http
User-Agent: dePeru.info_Calendario/1.0
```

Sustituye el valor por el nombre o dominio que te pertenece.

## cURL

```bash
curl --fail --silent --show-error \
  --max-time 10 \
  --user-agent 'dePeru.info_Calendario/1.0' \
  https://deperu.com/api/rest/calendarioPeru.json
```

## Python

Requiere Python 3.8 o posterior y usa la biblioteca estándar:

```python
import json
from urllib.error import HTTPError, URLError
from urllib.request import Request, urlopen

URL = "https://deperu.com/api/rest/calendarioPeru.json"
USER_AGENT = "dePeru.info_Calendario/1.0"

request = Request(
    URL,
    headers={
        "Accept": "application/json",
        "User-Agent": USER_AGENT,
    },
)

try:
    with urlopen(request, timeout=10) as response:
        data = json.loads(response.read().decode("utf-8"))
except HTTPError as error:
    raise SystemExit(f"El servidor respondió HTTP {error.code}") from error
except (URLError, TimeoutError) as error:
    raise SystemExit(f"No se pudo consultar el servicio: {error}") from error
except json.JSONDecodeError as error:
    raise SystemExit(f"La respuesta no contiene JSON válido: {error}") from error

if not isinstance(data, list):
    raise SystemExit("La respuesta JSON no es una lista de eventos.")

for evento in data:
    if not isinstance(evento, dict):
        continue
    print(f"{evento.get('fecha', 'Sin fecha')}: {evento.get('titulo', 'Sin título')}")
    print(evento.get("url", ""))
```

## PHP

Requiere PHP con la extensión cURL habilitada:

```php
<?php
$url = 'https://deperu.com/api/rest/calendarioPeru.json';
$userAgent = 'dePeru.info_Calendario/1.0';
$curl = curl_init($url);

curl_setopt_array($curl, [
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_CONNECTTIMEOUT => 5,
    CURLOPT_TIMEOUT => 10,
    CURLOPT_USERAGENT => $userAgent,
    CURLOPT_HTTPHEADER => ['Accept: application/json'],
]);

$body = curl_exec($curl);
$status = curl_getinfo($curl, CURLINFO_HTTP_CODE);
$error = curl_error($curl);
curl_close($curl);

if ($body === false) {
    throw new RuntimeException("Error de conexión: {$error}");
}
if ($status < 200 || $status >= 300) {
    throw new RuntimeException("El servidor respondió HTTP {$status}");
}

$data = json_decode($body, true);
if (!is_array($data) || json_last_error() !== JSON_ERROR_NONE) {
    throw new RuntimeException('La respuesta no contiene JSON válido.');
}

foreach ($data as $evento) {
    if (!is_array($evento)) {
        continue;
    }
    printf("%s: %s\n", $evento['fecha'] ?? 'Sin fecha', $evento['titulo'] ?? 'Sin título');
    if (!empty($evento['url'])) {
        printf("%s\n", $evento['url']);
    }
}
```

## Node.js

Requiere Node.js 18 o posterior, que incluye `fetch`:

```js
const url = "https://deperu.com/api/rest/calendarioPeru.json";
const userAgent = "dePeru.info_Calendario/1.0";

async function main() {
  let response;
  try {
    response = await fetch(url, {
      headers: {
        Accept: "application/json",
        "User-Agent": userAgent,
      },
      signal: AbortSignal.timeout(10_000),
    });
  } catch (error) {
    throw new Error(`No se pudo consultar el servicio: ${error.message}`);
  }

  if (!response.ok) {
    throw new Error(`El servidor respondió HTTP ${response.status}`);
  }

  let data;
  try {
    data = await response.json();
  } catch {
    throw new Error("La respuesta no contiene JSON válido.");
  }

  if (!Array.isArray(data)) {
    throw new Error("La respuesta JSON no es una lista de eventos.");
  }

  for (const evento of data) {
    if (!evento || typeof evento !== "object" || Array.isArray(evento)) continue;
    console.log(`${evento.fecha ?? "Sin fecha"}: ${evento.titulo ?? "Sin título"}`);
    if (evento.url) console.log(evento.url);
  }
}

main().catch((error) => {
  console.error(error.message);
  process.exitCode = 1;
});
```

## Java

Ejemplo de consulta para Java 11 o posterior con `HttpClient`. El cuerpo se imprime para que puedas analizarlo con la biblioteca JSON que ya use tu proyecto (por ejemplo, Jackson o Gson):

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.time.Duration;

public class CalendarioPeru {
    public static void main(String[] args) throws Exception {
        var client = HttpClient.newBuilder()
                .connectTimeout(Duration.ofSeconds(5))
                .build();
        var request = HttpRequest.newBuilder()
                .uri(URI.create("https://deperu.com/api/rest/calendarioPeru.json"))
                .timeout(Duration.ofSeconds(10))
                .header("Accept", "application/json")
                .header("User-Agent", "dePeru.info_Calendario/1.0")
                .GET()
                .build();

        var response = client.send(request, HttpResponse.BodyHandlers.ofString());
        if (response.statusCode() < 200 || response.statusCode() >= 300) {
            throw new IllegalStateException("El servidor respondió HTTP " + response.statusCode());
        }

        System.out.println(response.body());
    }
}
```

## Manejo de respuesta y errores

- Comprueba el código HTTP antes de interpretar el cuerpo.
- Usa un timeout para no dejar bloqueada la aplicación.
- Verifica que la respuesta JSON sea una lista y que cada elemento sea un objeto.
- Trata los campos opcionales o vacíos de forma segura.
- Escapa correctamente el texto al insertarlo en HTML y valida las URLs antes de crear enlaces o mostrar imágenes.

## Frecuencia y caché

El endpoint se describe como un calendario diario. Evita consultar en bucle y considera reutilizar en caché la respuesta del día. La frecuencia y duración de caché adecuadas dependen de las condiciones del proveedor y de los requisitos de tu aplicación.
