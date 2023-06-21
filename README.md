# Vue3 + Vite + PWA

Este es un proyecto que utiliza Vue 3, Vite  para crear una aplicación web progresiva (PWA).

## Pasos realizados

1. Instalación del plugin **vite-plugin-pwa**:
```js 
npm install -D vite-plugin-pwa
```
2. Configuración del archivo **vite.config.js**:
 ```js
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import { VitePWA } from 'vite-plugin-pwa'

export default defineConfig({
  plugins: [
    vue(),
    VitePWA({
      registerType: 'autoUpdate',
    })
  ],
})
 ```

 3. Generación de los favicons y archivos HTML. Utiliza el sitio web [realfavicongenerator.net](https://realfavicongenerator.net/)  para generar los favicons y archivos HTML requeridos.

 4. Copia los favicons y archivos HTML generados a la carpeta **public** de tu proyecto.

 5. Abre el archivo **site.webmanifest** que se encuentra en la carpeta public y edítalo de la siguiente manera:
 ```js
 {
    "name": "Prueba",
    "short_name": "Prueba",
    "start_url":"/",
    "icons": [
        {
            "src": "/android-chrome-192x192.png",
            "sizes": "192x192",
            "type": "image/png"
        },
        {
            "src": "/android-chrome-512x512.png",
            "sizes": "512x512",
            "type": "image/png"
        }
    ],
    "theme_color": "#ffffff",
    "background_color": "#ffffff",
    "display": "standalone"
}
```

5. Ejecuta el siguiente comando para iniciar el proyecto y tener la PWA funcionando.
```js
npm run dev
```

## Enlaces de interés
- [Documentación vite-plugin-pwa](https://vite-pwa-org.netlify.app/)

