<script setup>
import HelloWorld from './components/HelloWorld.vue'
import { initializeApp } from "firebase/app";
import { getMessaging, getToken, onMessage } from "firebase/messaging";
import Swal from 'sweetalert2/dist/sweetalert2';

const firebaseConfig = {
  apiKey: "AIzaSyADiNnBFLh9T-dbTcyvTbtA7DzpOehWO9M",
  authDomain: "hello-notification-b9b9a.firebaseapp.com",
  projectId: "hello-notification-b9b9a",
  storageBucket: "hello-notification-b9b9a.appspot.com",
  messagingSenderId: "1006161878424",
  appId: "1:1006161878424:web:e6339a00188317cc31dfed",
  measurementId: "G-8MTLB5E8K9"
};


const app = initializeApp(firebaseConfig);


// Get registration token. Initially this makes a network call, once retrieved
// subsequent calls to getToken will return from cache.
const messaging = getMessaging();
// const topic = 'penawaran';
// const registrationToken = [import.meta.env.VITE_REG_TOKEN];

// getMessaging().subscribeToTopic(registrationToken, topic)
// .then((response) => {
//   // See the MessagingTopicManagementResponse reference documentation
//   // for the contents of response.
//   console.log('Successfully subscribed to topic:', response);
// })
// .catch((error) => {
//   console.log('Error subscribing to topic:', error);
// });

onMessage(messaging, (payload) => {
  console.log('Message received. ', payload);
  Swal.fire({
    toast: true,
    position: 'top-end',
    showConfirmButton: false,
    // timer: 3000,
    // timerProgressBar: true,

    icon: 'warning',
    title: 'Input Validation',
    text: "TEST"
  });
  // ...
});

getToken(messaging, { vapidKey: import.meta.env.VITE_VAPID_KEY }).then((currentToken) => {
  if (currentToken) {
    // Send the token to your server and update the UI if necessary
    console.log("Token is:",currentToken);
    // ...
  } else {
    // Show permission request UI
    console.log('No registration token available. Request permission to generate one.');
    // ...
  }
}).catch((err) => {
  console.log('An error occurred while retrieving token. ', err);
  // ...
});

</script>

<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" />
</template>

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
