# FloryApp Backend 🌹 (con Google Gemini — GRATIS)

Este es el servidor que hace posible que el botón **"Analizar con IA"** funcione
cuando abres FloryApp.html fuera de Claude.ai (en tu celular, computador, o
subido a un hosting).

Usa **Google Gemini**, que tiene una capa gratuita real — no necesitas
tarjeta de crédito ni pagar nada para empezar.

## ¿Por qué necesito esto?

Ninguna API de IA puede llamarse directamente desde el navegador con tu
clave secreta — eso expondría tu clave a cualquiera que vea el código fuente
de la página. Por eso este servidor actúa de "intermediario": recibe la foto,
llama a Gemini con tu clave (que solo vive en el servidor, nunca en el
HTML), y devuelve el resultado.

## Paso 1 — Consigue tu clave de API de Gemini (gratis)

1. Ve a **https://aistudio.google.com**
2. Inicia sesión con tu cuenta de Google (la misma de Gmail sirve).
3. Click en **"Get API Key"** (arriba a la izquierda o en el menú).
4. Click en **"Create API Key"** → elige "Create in new project" si te lo pide.
5. Copia la clave generada (empieza con `AIza...`). Guárdala.

> ✅ No te pedirá tarjeta de crédito para el nivel gratuito. Hay un límite
> de peticiones por minuto y por día, pero para uso personal es más que
> suficiente.

## Paso 2 — Sube este proyecto a GitHub

1. Crea una cuenta gratis en **https://github.com** si no tienes.
2. Crea un repositorio nuevo, por ejemplo `floryapp-backend`.
3. Sube estos 4 archivos: `server.js`, `package.json`, `.env.example`, `README.md`.
   (Puedes arrastrar los archivos directamente en la web de GitHub con el
   botón "Add file" → "Upload files", no necesitas usar la terminal).

## Paso 3 — Despliega en Render.com (gratis)

1. Ve a **https://render.com** y crea una cuenta gratis (puedes usar tu
   cuenta de GitHub para entrar más rápido).
2. Click en **New +** → **Web Service**.
3. Conecta tu repositorio `floryapp-backend` de GitHub.
4. Configura:
   - **Name:** `floryapp-backend` (o el que quieras)
   - **Region:** la más cercana a ti
   - **Branch:** main
   - **Runtime:** Node
   - **Build Command:** `npm install`
   - **Start Command:** `npm start`
   - **Instance Type:** Free
5. Antes de darle a "Create", baja hasta **Environment Variables** y agrega:
   - **Key:** `GEMINI_API_KEY`
   - **Value:** tu clave `AIza...` del Paso 1
6. Click **Create Web Service**. Espera 2-3 minutos mientras despliega.
7. Cuando termine, Render te da una URL como:
   `https://floryapp-backend.onrender.com`
   Esa es la URL de tu backend — la vas a necesitar en el siguiente paso.

> ⚠️ Nota: en el plan gratis de Render, el servidor "duerme" tras 15 minutos
> sin uso y tarda ~30 segundos en despertar la primera vez que lo llamas.
> Es normal — solo espera un momento en el primer análisis del día.

## Paso 4 — Conecta FloryApp.html con tu backend

Abre tu archivo `FloryApp.html` y busca esta línea (cerca de la función
`analizarImagen`):

```javascript
const BACKEND_URL = "https://TU-BACKEND-AQUI.onrender.com/api/analizar";
```

Reemplaza `https://TU-BACKEND-AQUI.onrender.com` por la URL real que Render
te dio en el Paso 3. Guarda el archivo.

## Paso 5 — ¡Listo!

Abre el `FloryApp.html` actualizado en tu navegador (doble clic, o subiéndolo
a cualquier hosting simple como Netlify, GitHub Pages, etc.) y prueba el
botón "Analizar con IA". Ahora debería funcionar completamente gratis y
fuera de Claude.ai.

## Probar el backend directamente (opcional)

Si quieres confirmar que el servidor está vivo, visita en el navegador:
`https://TU-BACKEND-AQUI.onrender.com/` — debería mostrar
"FloryApp backend (Gemini) funcionando ✅".

## Costos

- **Render (hosting del servidor):** gratis en el plan Free.
- **Google Gemini API:** gratis en el nivel "Free tier" de aistudio.google.com,
  con límites de peticiones por minuto/día (suficiente para uso personal).
  Si algún día necesitas más volumen, puedes activar facturación en Google
  Cloud, pero para este proyecto no hace falta.

## Límites del nivel gratuito de Gemini

El nivel gratuito tiene límites de cuántas fotos puedes analizar por minuto
y por día (varían según el modelo). Si ves un error de "límite excedido",
espera un minuto e intenta de nuevo. Puedes revisar los límites actuales en
https://ai.google.dev/gemini-api/docs/rate-limits
