<template>
  <div class="home-container">
    <h1>Jordbruksverket prototyp form</h1>

    <div>
      <Navbar />
    </div>
    <div>
      <Form />
    </div>

  </div>
</template>

<script setup>
  import Navbar from "../components/Navbar.vue"
  import Form from "../components/Form.vue"
</script>

<style>
.h1 {
  display: flex;
  justify-content: center;
}
</style>
