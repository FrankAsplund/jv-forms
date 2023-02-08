<template>
  <div>
    <v-card>
      <v-tabs
        v-model="tab"
        bg-color="white"
        color="black"
      >
        <v-tab value="one">Grunduppgifter</v-tab>
        <v-tab value="two">Ansökan</v-tab>
        <v-tab value="three">Summering</v-tab>
        <v-tab value="four">Klar</v-tab>
      </v-tabs>

      <div class="bg-light-green-lighten-4 w-100">
      <v-card-text>
        <v-window v-model="tab">
          <v-window-item value="one">
            <Form /> 
          </v-window-item>
  
          <v-window-item value="two">
            <FormApply />
          </v-window-item>
  
          <v-window-item value="three">
            <FormSummary />
          </v-window-item>

          <v-window-item value="four">
            <FormDone />
          </v-window-item>
        </v-window>

        <!-- <div class="d-flex justify-center my-2">
              <v-btn value="two" size="large" color="green"> Nästa </v-btn>
          </div> -->

      </v-card-text>
    </div>

    
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
  import FormApply from "../components/FormApply.vue"
  import FormSummary from "../components/FormSummary.vue"
  import FormDone from "../components/FormDone.vue"
</script>

<style>
.h1 {
  display: flex;
  justify-content: center;
}
</style>
