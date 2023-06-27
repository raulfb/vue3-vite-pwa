<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <button @click="showNotification()">Notificacion</button>
  <HelloWorld msg="Vite + Vue" />
</template>
<script setup>
import HelloWorld from "./components/HelloWorld.vue";
navigator.serviceWorker.register("sw.js");
if (Notification.permission !== "granted") {
  Notification.requestPermission();
}

// addEventListener("notificationclick", (event) => {});

function showNotification() {
  Notification.requestPermission((result) => {
    if (result === "granted") {
      navigator.serviceWorker.ready.then((registration) => {
        registration.showNotification("Atención", {
          body: "Esto es una notificación",
          icon: "../public/android-chrome-512x512.png",
          actions: [
            { action: "aceptar", title: "Aceptar" },
            { action: "rechazar", title: "Rechazar" },
          ],
        });
      });
    }
  });
}

const channel = new BroadcastChannel("sw-mensajes");
channel.addEventListener("message", (event) => {
  console.log("Received", event.data.title);
  if (event.data.title == "aceptar") {
    console.log("Botón aceptar pulsado");
  }
  if (event.data.title == "rechazar") {
    console.log("Botón rechazar pulsado");
  }
});
</script>
<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
