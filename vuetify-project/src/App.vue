<template>
  <v-app>
    <Navbar />
    <router-view />
    <Footer />
  </v-app>
</template>

<script setup>
import Footer from "./components/Footer.vue";
import Navbar from "./components/Navbar.vue";
</script>
