<template>
  <div class="text-center">
    <v-dialog v-model="dialog" class="w-50 h-75">
      <template v-slot:activator="{ props }">
        <v-btn color="white" v-bind="props" icon="mdi-account"></v-btn>
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
          <v-btn color="primary" @click="login()">Log in</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script setup>
import { ref, reactive } from "vue";
import CustomBody from "./c-body.vue";
import { useVModel } from "@vueuse/core";
import axios from "axios";

const dialog = ref(false);

const user = reactive({
  username: "",
  password: "",
});

const props = defineProps({
  loggedIn: {
    type: Boolean,
    default: () => ({
      default: false,
    }),
  },
});

const emit = defineEmits(["update:loggedIn"]);
const loggedIn = useVModel(props, "loggedIn", emit);

function login() {
  if (user.username == "admin" && user.password == "admin") {
    console.log(user.username);
    console.log(user.password);
    loggedIn.value = true;
    console.log("You are now logged in");
  } else {
    console.log(user.username);
    console.log(user.password);
    console.log("Username and Password are incorrect");
  }
}

/* function login() {
  if (user.username == "admin" && user.password == "admin") {
    console.log(user.username);
    console.log(user.password);
    try {
      axios
        .post("http://localhost:8000/loginStatus", {
          status: true,
        })
        .then(function (response) {
          console.log(response, "Du är nu inloggad.");
        });
    } catch (error) {
      console.log(error);
    }
  } else {
    console.log(user.username);
    console.log(user.password);
    console.log("Username and Password are incorrect");
  }
} */
</script>
