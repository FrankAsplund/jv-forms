<template>
<div class="d-flex justify-center my-2">
    <h1 class="label">{{ header }}</h1>
</div>
<div class="d-flex justify-center my-2">
    <p class="label">{{  body }}</p>
</div>
</template>


<script>
export default {
  name: "Form-header",
  props: {
    header: {
      type: String,
    },
    body: {
      type: String,
    }
  },
};
</script>

<style>
.label {
    margin-bottom: 4px;
    font-family: 'Poppins', sans-serif;

}
</style>