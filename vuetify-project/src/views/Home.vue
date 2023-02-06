<template>
  <div class="home-container">

    <div class="d-flex justify-center">
      <h1>Fyll i formuläret</h1>
    </div>

    <v-card>
      <v-tabs
        v-model="tab"
        color="primary"
      >
        <v-tab value="one">Grunduppgifter</v-tab>
        <v-tab value="two">Ansökan</v-tab>
        <v-tab value="three">Summering</v-tab>
        <v-tab value="four">Klar</v-tab>
      </v-tabs>
  
      <v-card-text>
        <v-window v-model="tab">
          <v-window-item value="one">
            <Form /> 
          </v-window-item>
  
          <v-window-item value="two">
            Ansökan
          </v-window-item>
  
          <v-window-item value="three">
            Summering
          </v-window-item>

          <v-window-item value="four">
            Klar
          </v-window-item>
        </v-window>
      </v-card-text>
    </v-card>
    </div>
  </template>

<script>
export default {
  data: () => ({
    tab: null,
  })
}
</script>

<script setup>
  import Form from "../components/Form.vue"
</script>

<style>
.h1 {
  display: flex;
  justify-content: center;
}
</style>
