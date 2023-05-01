<template>
  <div class="text-center">
    <v-dialog v-model="dialog" width="auto">
      <template v-slot:activator="{ props }">
        <v-btn color="black" v-bind="props" icon="mdi-account"></v-btn>
      </template>

      <v-card>
        <v-card-text> Login </v-card-text>
        <v-card-actions>
          <v-btn color="error" block @click="dialog = false">Close</v-btn>
          <v-btn color="primary">Log in</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script setup>
import { ref } from "vue";

const dialog = ref(false);
</script>
