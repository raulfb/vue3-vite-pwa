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
      srcDir: 'src',
      filename: 'sw.js',
      registerType: 'autoUpdate',
      devOptions: {
      enabled: true,
      type: 'module',
    },
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

## Habilitar el entorno de desarrollo
Para habilitar el entorno de desarrollo edita el archivo vite.config.js y añade:
```js
devOptions: {
  enabled: true,
},
```

## Notificaciones Push

### Comprobar si están habilitadas

Para comprobar si están habilitadas y en caso de que no lo estén solicitar permiso.

```js
if (Notification.permission !== 'granted') {
    Notification.requestPermission();
}
```

### Mostrar notificación

```js
function showNotification() {
    Notification.requestPermission((result) => {
        if (result === "granted") {
            navigator.serviceWorker.ready.then((registration) => {
                registration.showNotification("Atención", {
                    body: "Esto es una notificación",
                    icon: "../public/android-chrome-512x512.png",
                    actions: [
                        { action: "Aceptar", title: "Aceptar" },
                        { action: "Rechazar", title: "Rechazar" },
                    ],
                });
            });
        }
    });
}

showNotification();
```
En el sw.js
```js

self.addEventListener("notificationclick", function (event) {
  console.log("notificación abierta");
});

self.addEventListener('notificationclick', (event) => {
  if (event.action === 'Aceptar') {
    console.log('Se ha pulsado en Aceptar');
    // Realiza las acciones correspondientes al aceptar la notificación
  } else if (event.action === 'Rechazar') {
    console.log('Se ha pulsado en Rechazar');
    // Realiza las acciones correspondientes al rechazar la notificación
  }
  event.notification.close(); // Cierra la notificación
});

```
## Enlaces de interés
- [Documentación vite-plugin-pwa](https://vite-pwa-org.netlify.app/)

