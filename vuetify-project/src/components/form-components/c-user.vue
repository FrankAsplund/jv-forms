<template>
  <div class="text-center">
    <v-dialog v-model="dialog" class="w-50 h-75">
      <template v-slot:activator="{ props }">
        <v-btn color="black" v-bind="props" icon="mdi-account"></v-btn>
      </template>

      <v-card>
        <custom-body class="pa-4" body="Logga in" />
        <v-card-text>
          <v-text-field
            v-model="user.username"
            label="Användarnamn"
            class="mb-2"
          />
          <v-text-field v-model="user.password" label="Lösenord" class="mb-2" />
        </v-card-text>
        <v-card-actions>
          <v-btn color="error" @click="dialog = false">Close</v-btn>
          <v-btn color="primary" @click="login">Log in</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script setup>
import { ref } from "vue";
import CustomBody from "./c-body.vue";
import { useVModel } from "@vueuse/core";

const dialog = ref(false);

const props = defineProps({
  user: {
    type: Object,
    default: () => ({
      username: "",
      password: "",
    }),
  },
});

const emit = defineEmits(["update:user"]);
const user = useVModel(props, "user", emit);

function login() {
  if (user.username == "admin" || user.password == "admin") {
    console.log("You are now logged in");
  } else {
    console.log("Username and Password are incorrect");
  }
}
</script>
