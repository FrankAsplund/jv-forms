<template>
  <v-alert type="success" variant="tonal">
    id: {{ responseId }} email: {{ responseEmail }}</v-alert
  >
</template>

<script setup>
import { onMounted } from "vue";

const props = defineProps({
  responseId: {
    type: Number,
  },
  responseEmail: {
    type: String,
  },
});

/* console.log(responseId); */

/* async function getData() {
  try {
    const response = await axios.get(
      `https://dummy.restapiexample.com/api/v1/${id}`,
      {
        headers: {
          "Content-Type": "application/json",
        },
      }
    );
    console.log(response.data);
  } catch (error) {
    console.log(error);
  }
} */

onMounted(() => {
  console.log(`the component is now mounted.`);
  /* getData(); */
});
</script>

<style scoped>
.line-divider {
  margin-top: 1.5rem;
  margin-bottom: 0.5rem;
  border-bottom: 2px solid rgb(156, 207, 111);
}
</style>
