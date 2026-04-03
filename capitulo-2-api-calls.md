# Capítulo 2 – API Calls y Herramientas (OpenAI)

## 1. El problema
Para muchos, el término **“API call”** se lanza en tutoriales sin una explicación real. Esto genera una barrera mental: los devs primerizos sienten que están conectando cables a ciegas.

* **El vacío de contexto:** Muchos comienzan pegando código sin entender que una API es, simplemente, un puente de comunicación.
* **Parálisis por elección:** Entre Node.js, Deno y Bun, es fácil perderse. Muchos terminan frustrados por no tener un entorno de trabajo claro desde el inicio.

> **Tip:** Muchos desarrolladores comienzan sin un entorno definido y pierden horas configurando herramientas en lugar de crear su primera solución.

---

## 2. Qué cubrimos

### 2.1 El ciclo de una petición (Request & Response)
No veas la API como algo abstracto. Mírala como un ciclo de mensajería de ida y vuelta:

* **Request (La solicitud):** Tu código envía un paquete con tres cosas: quién eres (**API key**), qué quieres (**instrucciones**) y cómo lo quieres (**parámetros**).  
* **Procesamiento:** El servidor de OpenAI recibe tu paquete, lo interpreta y genera una respuesta.  
* **Response (La respuesta):** El servidor te devuelve un paquete de datos. Tu trabajo es abrirlo y usar la información que viene dentro.

### 2.2 Herramientas: ¿Por qué Node.js?
Aunque existen alternativas modernas como Bun o Deno, en esta serie utilizaremos **Node.js**.

* **Estabilidad:** Es el estándar probado en la industria.  
* **Ecosistema:** Si tienes un problema, alguien ya lo resolvió en Node.js.  
* **Compatibilidad:** Las librerías oficiales de OpenAI se diseñan y prueban prioritariamente para Node.js.

### 2.3 Los pilares de una llamada funcional
Antes de escribir una línea, necesitas tener listos tres elementos:

* **Autenticación (API Key):** Tu firma digital. Sin ella, el servidor no te abrirá la puerta.
* **Parámetros (Input):** Los detalles. No es solo “haz algo”, es “usa este modelo y responde con este tono”.
* **Manejo de datos:** La respuesta llega en **JSON**, una estructura organizada (como una lista de etiquetas). Debes saber cómo extraer el valor que te interesa.

---

## 3. Ejemplo práctico

**Antes de correr este código, instala la librería en tu terminal:** `npm install openai`

```javascript
import OpenAI from "openai";

// 1. Configura tu API key en variables de entorno (más seguro que ponerla aquí)
const client = new OpenAI({
  apiKey: process.env.OPENAI_API_KEY
});

async function generarTexto() {
  try {
    // 2. Petición al modelo de Chat Completions
    const respuesta = await client.chat.completions.create({
      model: "gpt-4o-mini", // O gpt-3.5-turbo si no tienes acceso
      messages: [
        { role: "system", content: "Eres un asistente útil para programadores." },
        { role: "user", content: "Dame una idea breve para un proyecto de programación." }
      ]
    });

    // 3. Extraemos el mensaje generado
    console.log(respuesta.choices[0].message.content);

    // 4. (Opcional) para ver toda la estructura de la respuesta
    // console.log(JSON.stringify(respuesta, null, 2));

  } catch (error) {
    // Manejo preventivo de errores
    console.error("Algo no salió como esperábamos:", error.message);
  }
}

// 5. Ejecuta la función
generarTexto();
```


### ¿Qué está pasando realmente?

`await`: Le dice a tu programa: “espera un momento a que el servidor responda antes de continuar”. Sin esto, intentarías imprimir un resultado que aún no ha llegado de los servidores de OpenAI.

`respuesta.choices[0].message.content`: Las APIs devuelven un objeto con mucha información técnica (cuántos tokens usaste, qué modelo respondió, etc.). Esta ruta específica es la que llega directamente al texto que la IA generó para ti.

### 4. Errores comunes y Debugging

Incluso a los expertos les fallan las llamadas. La clave es saber leer los mensajes de error:

`Rate Limits (Límite de velocidad)`: Si envías demasiadas peticiones muy rápido, la API te pedirá que esperes. Es normal en cuentas gratuitas o nuevas. 

`Authentication Error`: Revisa que tu API Key no tenga espacios extra y que tu cuenta tenga saldo/créditos activos en OpenAI. 

`El paracaídas (try/catch)`: Siempre envuelve tus llamadas en este bloque. Si el internet falla, tu app no se cerrará de golpe, sino que te avisará qué pasó en el catch.

### 5. Siguiente paso

Ya dominas el texto, pero la IA también puede trabajar con otros formatos:

## Próximamente – Capítulo 3: Imágenes y archivos.
Aprenderemos a enviar imágenes y documentos PDF para que la IA genere respuestas basadas en archivos y en contenido visual real.

## Tu feedback cuenta:
Si este capítulo te sirvió o encontraste alguna traba, compártelo en el repositorio de GitHub. Mejorar la serie es un esfuerzo de comunidad.
