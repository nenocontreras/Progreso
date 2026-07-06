# Mi Progreso — PWA de Fitness & Racha 🔥

Aplicación web progresiva (PWA) instalable en **Android, iPhone, Windows y Mac** desde el navegador. Funciona **sin conexión** y guarda tu racha y tus registros en el dispositivo.

---

## 1. Estructura del proyecto

```
mi-progreso/
├── index.html          ← La app completa (interfaz + lógica + registro del Service Worker)
├── manifest.json       ← Ficha de la PWA: nombre, colores, íconos, cómo se instala
├── sw.js               ← Service Worker: caché y funcionamiento sin conexión
├── icons/
│   ├── icon-192.png            ← Ícono estándar 192×192 (Android/escritorio)
│   ├── icon-512.png            ← Ícono estándar 512×512 (splash y tiendas)
│   ├── icon-maskable-192.png   ← Ícono "maskable" 192 (Android recorta a cualquier forma)
│   ├── icon-maskable-512.png   ← Ícono "maskable" 512
│   ├── apple-touch-icon.png    ← Ícono para la pantalla de inicio de iPhone/iPad (180×180)
│   ├── favicon.svg             ← Favicon vectorial (pestaña del navegador)
│   └── favicon-32.png          ← Favicon PNG de respaldo (32×32)
├── screenshots/
│   ├── screenshot-narrow.png   ← Captura vertical (mejora el cartel de instalación en Android)
│   └── screenshot-wide.png     ← Captura horizontal (escritorio)
└── README.md           ← Este archivo
```

---

## 2. Para qué sirve cada archivo

- **index.html** — Es toda la aplicación en un solo archivo: la interfaz (estilo iOS), la lógica de la racha tipo Duolingo, el registro diario, los gráficos, el guardado de datos (`localStorage`), el registro del Service Worker y el botón "Instalar app". No necesita compilación ni dependencias.
- **manifest.json** — Le dice al navegador que esto es una app instalable: su nombre, el ícono, los colores de tema, la orientación y la pantalla de inicio. Sin él, no aparece la opción de instalar.
- **sw.js** (Service Worker) — Un script que corre en segundo plano. Guarda en caché los archivos de la app la primera vez que la abres, para que **funcione sin internet** y cargue al instante las siguientes veces.
- **icons/** — Los íconos que ves en la pantalla de inicio, el splash y la pestaña. Se incluyen versiones normales y *maskable* (Android las recorta en círculo, cuadrado redondeado, etc.).
- **screenshots/** — Imágenes opcionales que Android muestra en un cartel de instalación más atractivo. Puedes reemplazarlas por capturas reales de tu app.

---

## 3. Cómo probarla localmente

Una PWA necesita servirse por HTTP (no vale abrir el archivo con doble clic, porque el Service Worker no funciona con `file://`). Elige **una** opción:

**Opción A — Python (ya lo tienes en Mac/Linux):**
```bash
cd mi-progreso
python3 -m http.server 8080
```
Abre `http://localhost:8080` en el navegador.

**Opción B — Node.js:**
```bash
cd mi-progreso
npx serve .
```

**Opción C — VS Code:** instala la extensión "Live Server", clic derecho en `index.html` → "Open with Live Server".

> En `localhost` el Service Worker sí funciona aunque no haya HTTPS (es una excepción permitida). En producción **siempre** debe ser HTTPS (GitHub Pages, Netlify y Vercel ya lo dan gratis).

---

## 4. Publicarla gratis

### GitHub Pages
1. Crea un repositorio en GitHub (por ejemplo `mi-progreso`) y sube el contenido de la carpeta.
   ```bash
   cd mi-progreso
   git init
   git add .
   git commit -m "PWA Mi Progreso"
   git branch -M main
   git remote add origin https://github.com/TU_USUARIO/mi-progreso.git
   git push -u origin main
   ```
2. En GitHub: **Settings → Pages → Source: Deploy from a branch → Branch: `main` / carpeta `/root` → Save**.
3. En un minuto tendrás la URL: `https://TU_USUARIO.github.io/mi-progreso/`.
   > Como las rutas del proyecto son **relativas**, funciona perfecto en esa subcarpeta.

### Netlify (sin comandos)
1. Entra en app.netlify.com → **Add new site → Deploy manually**.
2. Arrastra la carpeta `mi-progreso` a la zona de subida.
3. Listo: te da una URL `https://algo.netlify.app` con HTTPS.
   (También puedes conectar tu repo de GitHub para que se actualice solo.)

### Vercel
1. Entra en vercel.com → **Add New → Project** → importa tu repositorio de GitHub (o usa `npx vercel` en la carpeta).
2. Framework preset: **Other**. No hace falta build. **Deploy**.
3. Te da una URL `https://algo.vercel.app` con HTTPS.

---

## 5. Cómo instalar la app (usuario final)

### 📱 Android (Chrome/Edge/Brave)
- Abre la URL. Aparecerá un aviso "Instalar app" o un ícono ⬇️ en la barra. Tócalo → **Instalar**.
- Si no aparece: menú **⋮ → Instalar app / Añadir a pantalla principal**.

### 🍎 iPhone / iPad (Safari — obligatorio Safari)
1. Abre la URL en **Safari**.
2. Toca el botón **Compartir** (cuadro con flecha ↑).
3. Elige **Añadir a inicio**.
4. Toca **Añadir**. Aparecerá el ícono en tu pantalla, a pantalla completa.
   > iOS no muestra un botón automático de instalar; siempre es por "Compartir". La app ya incluye estas instrucciones dentro de Ajustes.

### 🪟 Windows (Chrome/Edge)
- Abre la URL → ícono **⊕/⬇️ "Instalar"** al final de la barra de direcciones → **Instalar**.
- O menú **⋮ → Apps → Instalar este sitio como aplicación**. Quedará en el menú Inicio.

### 💻 Mac (Chrome/Edge)
- Abre la URL → ícono **⬇️ "Instalar"** en la barra → **Instalar**. Aparece en Launchpad/Dock.
- **Safari en Mac (Sonoma+):** menú **Archivo → Añadir al Dock**.

---

## 6. Lista de comprobación (checklist PWA)

- [x] `manifest.json` enlazado en el HTML (`<link rel="manifest">`)
- [x] `name`, `short_name`, `start_url`, `scope` y `display: standalone`
- [x] `theme_color` y `background_color` definidos
- [x] Íconos 192 y 512 (any) + versiones **maskable**
- [x] `apple-touch-icon` y metadatos de iOS (`apple-mobile-web-app-*`)
- [x] Favicon (SVG + PNG)
- [x] Service Worker registrado y con caché del app shell
- [x] Funciona **sin conexión** (prueba: activa modo avión y recárgala)
- [x] Rutas **relativas** (funciona en subcarpetas como GitHub Pages)
- [x] Botón/entrada de instalación dentro de la app
- [x] Datos persistentes en el dispositivo (`localStorage`)
- [ ] Servida por **HTTPS** en producción (lo dan GitHub Pages/Netlify/Vercel)
- [ ] (Opcional) Reemplazar `screenshots/` por capturas reales de tu app

**Cómo verificar rápido:** en Chrome, abre **DevTools (F12) → pestaña "Application" → Manifest** y **Service Workers**. Y en **Lighthouse**, corre la auditoría "Progressive Web App".

---

## 7. Notas importantes

- **Persistencia de datos:** la app guarda tu racha y registros con `localStorage`, en el navegador donde la instales. Para no perderlos, úsala siempre desde el mismo dispositivo/navegador (idealmente la app ya instalada). Borrar los datos del navegador borra la app. Si en el futuro quieres sincronizar entre varios dispositivos, haría falta una cuenta y un servidor (por ejemplo Firebase o Supabase).
- **Actualizar la app tras cambios:** si modificas archivos, sube el número de versión en `sw.js` (cambia `mi-progreso-v1` por `-v2`). Así el Service Worker renueva la caché y todos ven la versión nueva.
- **Reemplazar íconos:** si quieres tu propio logo, sustituye los PNG de `icons/` manteniendo los mismos nombres y tamaños. Para regenerarlos fácilmente puedes usar una herramienta como [maskable.app](https://maskable.app) o [realfavicongenerator.net](https://realfavicongenerator.net).

---

Hecho para tu transformación. 💪
