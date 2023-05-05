<template>
  <div class="mb-16">
    <v-app-bar>
      <template v-slot:prepend>
        <User v-model:loggedIn="loggedIn" />

        <Admin v-if="loggedIn" />

        <v-btn icon="mdi-magnify"></v-btn>

        <v-btn icon="mdi-dots-vertical"></v-btn>
      </template>
    </v-app-bar>
  </div>
</template>

<script setup>
import User from "./form-components/c-user.vue";
import Admin from "./form-components/c-admin.vue";
/* import { ref, reactive } from "vue"; */

/* const user = reactive({
  username: "",
  password: "",
}); */
</script>
