<template>
  <custom-header header="Tack för din ansökan!" />
  <v-alert type="success" variant="tonal">
    <pre>
        Ditt casenummer är {{ responseData }}  
      </pre
    >
  </v-alert>
  <v-btn class="ma-4" color="primary" @click="refreshPage()">Ny ansökan</v-btn>
</template>

<script setup>
import CustomHeader from "../form-components/c-header.vue";

defineProps({
  responseData: {
    type: Object,
    default: null,
  },
});

function refreshPage() {
  location.reload();
}
</script>

<style scoped>
.line-divider {
  margin-top: 1.5rem;
  margin-bottom: 0.5rem;
  border-bottom: 2px solid rgb(156, 207, 111);
}
</style>
