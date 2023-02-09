<template>
  <div class="bg-light-green-lighten-4 w-100">
    <v-container class="rounded mx-12">
      <v-card>
        <v-toolbar class="bg-light-blue-lighten-5 w-100 text-h5 font-weight-bold justify-center" dark>
          <v-toolbar-title>{{ currentTitle }}
            <v-avatar class="mx-4" color="primary" size="36" v-text="step"></v-avatar>
          </v-toolbar-title>

      <v-breadcrumbs :items="items">
        <template v-slot:title="{ item }">
          {{ currentPage }}
          {{ item.title }}
        </template>
      </v-breadcrumbs>


    </v-toolbar>

      <v-window v-model="step" class="mx-12">
      <v-window-item :value="1">
        <Form />
      </v-window-item>

      <v-window-item :value="2">
        <FormApply />
      </v-window-item>
      
      <v-window-item :value="3">
        <FormSummary />
      </v-window-item>
      
      <v-window-item :value="4">
        <FormDone />
      </v-window-item>
      
    </v-window>
    <v-card-actions>
      <v-btn v-if="step > 1" variant="tonal" width="200" size="large" @click="step--">Tillbaka</v-btn>
      <v-spacer></v-spacer>
      <v-btn v-if="step < 4" size="large" color="green" width="200" variant="tonal" @click="step++">Nästa</v-btn>
    </v-card-actions>
  </v-card>
  </v-container>
  </div>
</template>

<script>
  export default {
    data: () => ({
      step: 1,
      items: [
          {
            id: 0,
            title: 'Grunduppgifter',
            disabled: false,
          },
          {
            id: 1,
            title: 'Ansökan',
            disabled: true,
          },
          {
            id: 2,
            title: 'Summering',
            disabled: true,
          },
          {
            id: 3,
            title: 'Klar',
            disabled: true,
          },
        ],
    }),

    computed: {

      currentPage() {
        switch (this.step) {
          case 1: this.items[0].disabled = false, 
          this.items[1].disabled = true, 
          this.items[2].disabled = true, 
          this.items[3].disabled = true
          
          case 2:

          return this.items[0].disabled = true, 
          this.items[1].disabled = false, 
          this.items[2].disabled = true, 
          this.items[3].disabled = true

          case 3: 
          this.items[0].disabled = true, 
          this.items[1].disabled = true, 
          this.items[2].disabled = false, 
          this.items[3].disabled = true

          case 4: 
          this.items[0].disabled = true, 
          this.items[1].disabled = true, 
          this.items[2].disabled = true, 
          this.items[3].disabled = false
        }
      },

      currentTitle () {
        switch (this.step) {
          case 1: return 'Grunduppgifter'
          case 2: return 'Ansökan'
          case 3: return 'Summering'
          case 4: return 'Klar'
        }
      },
    },
  }
</script>

<script setup>
  import Form from "../components/Form.vue"
  import FormApply from "../components/FormApply.vue"
  import FormSummary from "../components/FormSummary.vue"
  import FormDone from "../components/FormDone.vue"

/*   import FormHeader from "../components/form-components/c-header.vue"
  import FormBodyText from "../components/form-components/c-body.vue" */
</script>

<style>
</style>
