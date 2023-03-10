<template>
  <v-alert type="success" variant="tonal">
    <pre>
      {{ responseData.data }}  
    </pre>
  </v-alert>
</template>

<script setup>
const props = defineProps({
  responseData: {
    type: Object,
  },
});
</script>

<style scoped>
.line-divider {
  margin-top: 1.5rem;
  margin-bottom: 0.5rem;
  border-bottom: 2px solid rgb(156, 207, 111);
}
</style>
