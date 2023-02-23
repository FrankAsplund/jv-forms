<template>
  <div class="d-flex bg-light-green-lighten-4 justify-center h-100">
    <v-container class="rounded mx-12">
      <v-card class="rounded-t-lg">
        <v-toolbar
          class="bg-light-blue-lighten-5 text-h5 font-weight-bold justify-center elevation-4"
          dark
        >
          <v-breadcrumbs :items="items">
            <template v-slot:title="{ item }">
              {{ item.title }}
            </template>
          </v-breadcrumbs>
          <v-toolbar-title class="text-h5 font-weight-bold"
            >{{ currentTitle }}
          </v-toolbar-title>
        </v-toolbar>

        <v-card-actions>
          <v-btn
            v-if="step > 1"
            size="x-large"
            icon="mdi-arrow-left-bold"
            color="black"
            @click="step--"
          ></v-btn>
          <v-spacer></v-spacer>
          <v-btn
            v-if="step < 4"
            size="x-large"
            icon="mdi-arrow-right-bold"
            color="black"
            @click="step++"
          ></v-btn>
        </v-card-actions>

        <v-window v-model="step" class="mx-12">
          <v-window-item :value="1">
             <Form :formData="formData" @submit.prevent="submitForm" />
          </v-window-item>

          <v-window-item :value="2">
            <FormApply :formData="formData" />
          </v-window-item>

          <v-window-item :value="3">
            <FormSummary />
          </v-window-item>

          <v-window-item :value="4">
            <FormDone />
          </v-window-item>
        </v-window>
      </v-card>
    </v-container>
  </div>
</template>

<script setup>
import Form from "../components/Form.vue";
import FormApply from "../components/FormApply.vue";
import FormSummary from "../components/FormSummary.vue";
import FormDone from "../components/FormDone.vue";
import { reactive } from "vue";
import axios from "axios";

const formData = reactive({
  firstname: "John",
  lastname: "Doe",
  ssn: "12456-1234",
  email: "",
  apply: "",
  applyCounty: "",
  applyNumber: "",
});

async function submitForm() {
  const data = { ...formData };
  try {
    const response = await axios.post(
      "https://dummy.restapiexample.com/api/v1/create",
      data,
      {
        headers: {
          "Content-Type": "application/json",
        },
      }
    );

    console.log(response.data);
    document.forms[0].reset();
  } catch (error) {
    console.log(error);
  }
}
</script>

<script>
export default {
  components: {
    Form,
    FormApply,
    FormSummary,
    FormDone,
  },
  name: "Home",
  data() {
    return {
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
    };
  },

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
    },

    currentItem() {
      return this.items[this.step - 1];
    },
  },
};
</script>

<style></style>
