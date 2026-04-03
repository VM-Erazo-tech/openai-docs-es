# ¿Qué es el SDK de OpenAI y por qué lo necesitas?

La documentación oficial asume que sabes qué es un SDK, pero si estás empezando, esto puede ser confuso.

Un SDK (Software Development Kit) es básicamente un conjunto de herramientas que te permite usar una tecnología sin tener que construir todo desde cero. En este caso, el SDK de OpenAI te facilita comunicarte con la API de forma sencilla, sin preocuparte por detalles técnicos complejos.

## ¿Qué es una API key?

Una API key es como una contraseña que identifica tu aplicación cuando intenta usar la API.

Sirve para que el sistema sepa quién está haciendo la solicitud, controlar el uso y evitar accesos no autorizados.

## ¿Qué es una variable de entorno?

Las variables de entorno (env vars) son valores que se guardan en tu sistema y que las aplicaciones pueden usar mientras se ejecutan.

Son útiles para almacenar información sensible, como tu API key, sin tener que escribirla directamente en el código.

# Instalación y configuración básica de la API key

Dependiendo de tu sistema operativo, el comando cambia:

### macOS / Linux
```bash
npm install openai
export OPENAI_API_KEY="tu_api_key"
```
### Windows (PowerShell)
```bash
$env:OPENAI_API_KEY="tu_api_key"
```

En ambos casos, este comando guarda tu API key como una variable de entorno, lo que permite que el sistema la use automáticamente sin tener que escribirla directamente en el código.
Esto evita tener que escribir tu clave manualmente cada vez.

## ¿Qué es npm?

Npm es una herramienta que consiste en un administrador de paquetes que permite a los desarrolladores de JavaScript trabajar con lo que llamamos dependencias. Estas dependencias, son como librerías que usamos para desarrollar un programa y nos ahorra empezar desde cero, su trabajo es muy amplio y te puede ayudar a: instalar, publicar y gestionar módulos en modo general

## Error común

Un error frecuente es escribir la API key directamente en el código. Esto es inseguro, ya que si compartes tu código, otras personas podrían usar tu clave.

Por eso se recomienda usar variables de entorno.

## Siguiente paso: tu primera API call

Una vez que tienes el SDK instalado y tu API key configurada, puedes realizar tu primera API call.

Esto significa hacer una petición a la inteligencia artificial para obtener una respuesta, como generar texto, analizar información o automatizar tareas. Es el punto donde pasas de la configuración a usar realmente la API.

### Ejemplo completo: tu primera API call

Crea un archivo llamado `example.js` y añade el siguiente código:

```javascript
import OpenAI from "openai";
const client = new OpenAI();

const response = await client.responses.create({
  model: "gpt-4",
  input: "Di hola en español"
});

console.log(response.output_text);
```

Luego ejecútalo en tu terminal con:

```bash
node example.js
```

## Si algo no funciona

Si tienes problemas al ejecutar estos pasos, revisa lo siguiente:

- Asegúrate de tener Node.js instalado (incluye npm).
- Verifica que tu API key esté correctamente escrita.
- Confirma que guardaste la variable de entorno antes de ejecutar el código.
- Reinicia tu terminal si hiciste cambios recientes.
