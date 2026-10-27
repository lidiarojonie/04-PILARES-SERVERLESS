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