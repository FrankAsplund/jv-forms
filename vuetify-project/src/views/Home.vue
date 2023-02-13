<template>
  <div class="d-flex bg-light-green-lighten-4 justify-center h-100">
    <v-container class="rounded mx-12">
      <v-card class="rounded-t-lg">
        <v-toolbar
          class="bg-light-blue-lighten-5 text-h5 font-weight-bold justify-center elevation-6"
          dark
        >
          <v-toolbar-title class="text-h5 font-weight-bold"
            >{{ currentTitle }}
            <v-avatar
              class="text-h6 mx-4"
              color="light-blue-lighten-3"
              size="28"
              v-text="step"
            ></v-avatar>
          </v-toolbar-title>

          <v-breadcrumbs :items="items">
            <template v-slot:title="{ item }">
              <v-btn variant="text" class="pa-0" color="light-blue-darken-4">
                {{ item.title }}
              </v-btn>
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
          <v-btn
            v-if="step > 1"
            variant="tonal"
            color="primary"
            width="200"
            size="large"
            @click="step--"
            >Tillbaka</v-btn
          >
          <v-spacer></v-spacer>
          <v-btn
            v-if="step < 4"
            size="large"
            color="success"
            width="200"
            variant="tonal"
            @click="step++"
            >Nästa</v-btn
          >
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
        title: "Grunduppgifter",
        disabled: false,
      },
      {
        title: "Ansökan",
        disabled: true,
      },
      {
        title: "Summering",
        disabled: true,
      },
      {
        title: "Klar",
        disabled: true,
      },
    ],
  }),

  methods: {
    updateDisabled() {
      this.items.forEach((item, index) => {
        item.disabled = index !== this.step - 1;
      });
    },
  },
  computed: {
    currentTitle() {
      this.updateDisabled(); // Update disabled property based on current step
      return this.currentItem.title; // Return title of current item
    },

    currentItem() {
      return this.items[this.step - 1];
    },
  },
};
</script>

<script setup>
import Form from "../components/Form.vue";
import FormApply from "../components/FormApply.vue";
import FormSummary from "../components/FormSummary.vue";
import FormDone from "../components/FormDone.vue";
</script>

<style></style>
