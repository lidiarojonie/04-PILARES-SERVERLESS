# 04-PILARES-SERVERLESS
 
# Festival Control · Bloque 01

## Qué he construido
He construido mi primera función Serverless (AWS Lambda) y la he ejecutado en local utilizando el plugin *Serverless Offline*. La ruta local que he probado ha sido un endpoint HTTP GET en `http://localhost:3000/dev/hello`

## Qué he comprendido
- **Tipos del handler:** Se usan tipos específicos (como `APIGatewayProxyEvent` y `APIGatewayProxyResult`) para tipar la entrada y salida, asegurando que la función se comunique correctamente con el formato de API Gateway.
- **La compilación:** Como el código se escribe en TypeScript, primero debe compilarse (transpilarse) a JavaScript puro para que el entorno de Node.js pueda entenderlo y ejecutarlo.
- **EVENT RECIBIDO:** Este mensaje aparece en la **terminal** donde está corriendo el servidor local (`serverless offline`), ya que es un `console.log` interno del backend y no parte de la respuesta que se envía al cliente.

## Qué he modificado
He modificado el mensaje dentro del objeto JSON en el cuerpo (`body`) de la respuesta de la función en el código. La URL no cambió porque la ruta del endpoint se define en la configuración de eventos del archivo `serverless.yml`, el cual se mantuvo intacto.

## Cómo lo he comprobado
- **Thunder Client:** Hice una petición a la ruta local y recibí un código de estado `200 OK` con el JSON actualizado.
- **curl:** Lancé la petición desde la terminal y obtuve exactamente la misma respuesta JSON.
- **Log:** Comprobé la consola del servidor y vi el registro del evento ejecutado con éxito.


# Bloque 02

## Resultado
- Qué añadí al proyecto: Un endpoint GET para obtener información del destino.
- Ruta o pantalla comprobada: La ruta GET del endpoint creado.
- Estado y respuesta observados: Comprobé la respuesta de la API mediante una petición GET.

## Comprensión
- Recorrido del dato: La petición llega al endpoint, se procesa y devuelve una respuesta al cliente.
- Cambio guiado y resultado: Modifiqué el endpoint siguiendo las instrucciones del ejercicio y comprobé el resultado.
- Error encontrado y cómo lo resolví: Revisé el código y la petición para localizar y corregir posibles errores.

## Evidencias
- Captura o transcripción breve, sin credenciales: 
curl -i http://localhost:3000/dev/events/EVT-330
HTTP/1.1 200 OK
content-type: application/json; charset=utf-8
vary: origin
access-control-expose-headers: WWW-Authenticate,Server-Authorization
cache-control: no-cache
content-length: 95
accept-ranges: bytes
Date: Wed, 28 Oct 2026 18:07:10 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{"id":"EVT-330","artist":"Neon Waves","space":"Main Stage","time":"22:30","status":"CONFIRMED"}

- Limitaciones del ejercicio: Funcionalidad limitada a lo implementado en el ejercicio.


# Bloque 03

## Resultado
- Qué añadí al proyecto: Un endpoint POST para enviar datos de un destino.
- Ruta o pantalla comprobada: La ruta POST del endpoint de destino.
- Estado y respuesta observados: Probé el envío de datos mediante una petición POST.

## Comprensión
- Recorrido del dato, explicado con mis palabras: El cliente envía los datos en la petición, el endpoint los procesa y devuelve una respuesta.
- Cambio guiado y resultado: Seguí los pasos para construir y probar el endpoint POST.
- Error encontrado y cómo lo resolví: Revisé los datos enviados y la petición para detectar posibles errores.

## Evidencias
- Captura o transcripción breve, sin credenciales: 
curl -i -X POST http://localhost:3000/dev/events -H 'Content-Type: application/json' -d '{"artist":"Nova Pulse","space":"Main Stage","time":"21:00","status":"CANCELLED"}'
HTTP/1.1 201 Created
content-type: application/json; charset=utf-8
vary: origin
access-control-expose-headers: WWW-Authenticate,Server-Authorization
cache-control: no-cache
content-length: 95
Date: Wed, 28 Oct 2026 18:18:54 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{"id":"EVT-NEW","artist":"Nova Pulse","space":"Main Stage","time":"21:00","status":"CANCELLED"}

curl -i -X POST http://localhost:3000/dev/events -H 'Content-Type: application/json' -d '{"artist":"Nova Pulse","space":"Main Stage","time":"21:00","status":"PAUSED"}'
HTTP/1.1 400 Bad Request
content-type: application/json; charset=utf-8
vary: origin
access-control-expose-headers: WWW-Authenticate,Server-Authorization
cache-control: no-cache
content-length: 51
Date: Wed, 28 Oct 2026 18:19:25 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{"message":"status debe ser CONFIRMED o CANCELLED"}

curl -i -X POST http://localhost:3000/dev/events -H 'Content-Type: application/json' -d '{"artist":"Nova Pulse","space":"Main Stage","time":"29:80","status":
"CANCELLED"}'
HTTP/1.1 400 Bad Request
content-type: application/json; charset=utf-8
vary: origin
access-control-expose-headers: WWW-Authenticate,Server-Authorization
cache-control: no-cache
content-length: 59
Date: Wed, 28 Oct 2026 18:19:47 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{"message":"artist, space y time (HH:mm) son obligatorios"}

- Limitaciones del ejercicio: Funcionalidad limitada a las operaciones implementadas en el ejercicio.


# Bloque 04

## Resultado
- Qué añadí al proyecto: Operaciones CRUD para gestionar destinos.
- Ruta o pantalla comprobada: Endpoints de destino para crear, consultar, modificar y eliminar datos.
- Estado y respuesta observados: Probé las operaciones y comprobé las respuestas de la API.

## Comprensión
- Recorrido del dato, explicado con mis palabras: La API recibe la petición, procesa la operación sobre los datos y devuelve una respuesta.
- Cambio guiado y resultado: Implementé las operaciones CRUD siguiendo los pasos del ejercicio.
- Error encontrado y cómo lo resolví: Revisé las peticiones y los datos enviados para corregir posibles errores.

## Evidencias
- Captura o transcripción breve, sin credenciales: 
curl -i -X PUT http://localhost:3000/dev/events/EVT-101 -H 'Content-Type: application/json' -d '{"status":"CONFIRMED"}'
HTTP/1.1 400 Bad Request
content-type: application/json; charset=utf-8
vary: origin
access-control-expose-headers: WWW-Authenticate,Server-Authorization
cache-control: no-cache
content-length: 69
Date: Wed, 28 Oct 2026 18:39:03 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{"message":"PUT requiere artist, space, time HH:mm y status válido"}

curl -i -X PATCH http://localhost:3000/dev/events/EVT-101 -H 'Content-Type: application/json' -d '{"status":"CONFIRMED"}'
HTTP/1.1 200 OK
content-type: application/json; charset=utf-8
vary: origin
access-control-expose-headers: WWW-Authenticate,Server-Authorization
cache-control: no-cache
content-length: 71
Date: Wed, 28 Oct 2026 18:39:32 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{"id":"EVT-101","changes":{"status":"CONFIRMED"},"operation":"UPDATED"}

curl -i http://localhost:3000/dev/events/EVT-101
HTTP/1.1 200 OK
content-type: application/json; charset=utf-8
vary: origin
access-control-expose-headers: WWW-Authenticate,Server-Authorization
cache-control: no-cache
content-length: 95
accept-ranges: bytes
Date: Wed, 28 Oct 2026 18:39:56 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{"id":"EVT-101","artist":"Neon Waves","space":"Main Stage","time":"22:30","status":"CONFIRMED"}

- Limitaciones del ejercicio: Funcionalidad limitada a las operaciones implementadas en el ejercicio.


# Bloque 05

## Resultado
- Qué añadí al proyecto: Una aplicación móvil con React Native para trabajar con destinos.
- Ruta o pantalla comprobada: Pantalla de destinos de la aplicación.
- Estado y respuesta observados: Comprobé el funcionamiento de la pantalla y la comunicación con la API.

## Comprensión
- Recorrido del dato, explicado con mis palabras: La aplicación envía peticiones a la API, recibe los datos y los muestra en pantalla.
- Cambio guiado y resultado: Construí y modifiqué la aplicación siguiendo los pasos del ejercicio.
- Error encontrado y cómo lo resolví: Revisé el código y las peticiones para solucionar posibles errores.

## Evidencias
- Limitaciones del ejercicio: Funcionalidad limitada a las pantallas y operaciones implementadas.


# Bloque 06

## Resultado
- Qué añadí al proyecto: La consulta de destinos desde React Native mediante una petición GET.
- Ruta o pantalla comprobada: Pantalla de destinos de la aplicación móvil.
- Estado y respuesta observados: Comprobé la petición y la recepción de datos desde la API.

## Comprensión
- Recorrido del dato, explicado con mis palabras: La aplicación realiza una petición GET, recibe los datos de la API y los muestra en pantalla.
- Cambio guiado y resultado: Implementé y probé la consulta siguiendo los pasos del ejercicio.
- Error encontrado y cómo lo resolví: Revisé la URL y la petición para detectar posibles errores de conexión.

## Evidencias
- Captura o transcripción breve, sin credenciales: HTTP 404: Not Found
- Limitaciones del ejercicio: Se limita a consultar y mostrar los datos disponibles en la API.


# Bloque 07

## Resultado
- Qué añadí al proyecto: La gestión de destinos desde React Native mediante operaciones CRUD.
- Ruta o pantalla comprobada: Pantalla de gestión de destinos de la aplicación móvil.
- Estado y respuesta observados: Comprobé las operaciones para crear, consultar, modificar y eliminar destinos.

## Comprensión
- Recorrido del dato, explicado con mis palabras: La aplicación envía peticiones a la API, que procesa los cambios y devuelve una respuesta.
- Cambio guiado y resultado: Implementé las operaciones CRUD siguiendo los pasos del ejercicio.
- Error encontrado y cómo lo resolví: Revisé las peticiones y los datos enviados para detectar posibles errores.

## Evidencias
- Captura o transcripción breve, sin credenciales: 
PATCH cancelar EVT-101
{
  "id": "EVT-101",
  "changes": {
    "status": "CONFIRMED"
  },
  "operation": "UPDATED"
}

- Limitaciones del ejercicio: Funcionalidad limitada a las operaciones implementadas en el ejercicio.


