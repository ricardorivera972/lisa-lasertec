# Lisa Lasertec — Interfaz protegida (Vercel)

Interfaz mínima con **contraseña de acceso** y **proxy** a OpenAI para tu GPT *Lisa*.
Funciona en Vercel con un flujo simple: página estática + función serverless `/api/chat`.

## 🚀 Despliegue rápido (ZIP en Vercel)
1. Entrá a [vercel.com](https://vercel.com) e iniciá sesión.
2. Clic en **Add New… → Project → Import → Drag & Drop** y soltar este ZIP.
3. En **Environment Variables** agregá:
   - `OPENAI_API_KEY` → tu key de OpenAI.
   - `ACCESS_PASSWORD` → `LASER2025` (o la que quieras usar).
4. Deploy.

> Con esto, cualquiera que tenga el **enlace** necesitará además la **contraseña** para usar Lisa.

## 🧩 Cómo funciona
- `index.html` → UI con pantalla de contraseña y chat.
- `api/chat.js` → función serverless que:
  - Verifica la cabecera `x-passcode` contra `ACCESS_PASSWORD` (servidor).
  - Llama a **OpenAI** con `OPENAI_API_KEY`.
  - Devuelve el texto de respuesta al frontend.

## 🔐 Seguridad
- La contraseña se **valida en el servidor** (no sólo en el frontend).
- Sin la cabecera correcta `x-passcode`, el endpoint responde **401 No autorizado**.
- Tu API Key de OpenAI **no** se expone al navegador.

## 🧪 Prueba local (opcional)
Requiere Node 18+.
```bash
# Instalar deps opcionales (no estrictamente necesario para Vercel)
npm init -y
npm install --save-dev vercel
# Variables de entorno
cp .env.example .env
# Editá .env con tu OPENAI_API_KEY y ACCESS_PASSWORD
npx vercel dev
```
Abrí http://localhost:3000 y probá con tu contraseña.

## 🎨 Branding
- Podés editar colores, logo y textos directamente en `index.html`.
- Si querés imágenes/estilos adicionales, agregalas y Vercel las servirá de forma estática.

## ❌ Evitar duplicación de tu GPT
- Esta interfaz **no permite clonar** tu GPT. Es un frontend propio que consume la API.
- Aunque reenvíen el **enlace**, **sin la contraseña** no pueden usarlo.

## 🆘 Soporte
Si algo falla en el deploy (CORS, env vars, etc.), revisá el panel de logs de Vercel.
