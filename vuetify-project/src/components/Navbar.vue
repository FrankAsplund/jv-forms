<template>
  <div class="mb-16">
    <v-app-bar class="bg-grey-darken-4">
      <template v-slot:prepend>
        <User v-model:logged-in="loggedIn" />

        <Admin v-if="loggedIn">
          <RouterLink to="/Admin" />
        </Admin>

        <v-btn icon="mdi-magnify"></v-btn>

        <v-btn icon="mdi-dots-vertical"></v-btn>
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
