<template>
  <div class="mb-16">
    <v-app-bar class="bg-indigo-darken-1">
      <template v-slot:prepend>
        <v-btn to="/" icon="mdi-home" />

        <User v-model:logged-in="loggedIn" />

        <Admin v-if="loggedIn" />

        <v-btn icon="mdi-magnify"></v-btn>

        Hälsoundersökning
      </template>
    </v-app-bar>
  </div>
</template>

<script setup>
import User from "./form-components/c-user.vue";
import Admin from "./form-components/c-admin.vue";
import { ref, reactive } from "vue";

const loggedIn = ref(false);
</script>
