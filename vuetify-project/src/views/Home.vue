<template>
  <div class="d-flex bg-light-green-lighten-4 justify-center h-100">
    <v-container class="rounded mx-12">
      <v-card class="rounded-t-lg">
        <v-toolbar class="bg-light-blue-lighten-5 text-h5 font-weight-bold justify-center elevation-4" dark>
          <v-breadcrumbs :items="items">
            <template v-slot:title="{ item }">
              {{ item.title }}
            </template>
          </v-breadcrumbs>
          <v-toolbar-title class="text-h5 font-weight-bold"> </v-toolbar-title>
        </v-toolbar>

        <v-card-actions>
          <v-btn v-if="step > 1" size="x-large" icon="mdi-arrow-left-bold" color="black" @click="step--"></v-btn>
          <v-spacer></v-spacer>
          <v-btn v-if="step < 4" size="x-large" icon="mdi-arrow-right-bold" color="black" @click="step++"></v-btn>
        </v-card-actions>

        <v-window v-model="step" class="mx-12">
          <v-window-item :value="1">
            <Form v-model:formDataObj="formData" />
          </v-window-item>

          <v-window-item :value="2">
            <FormApply v-model:formDataApplyObj="formDataApply" />
          </v-window-item>

          <v-window-item :value="3">
            <FormSummary :form-data="formData" :form-data-apply="formDataApply" @submit-all="submitForm()" />
          </v-window-item>

          <v-window-item :value="4">
            <FormDone :responseData="responseData" />
          </v-window-item>
        </v-window>
        <v-card-actions>
          <v-btn v-if="step > 1" size="large" prepend-icon="mdi-arrow-left-bold" color="light-blue-accent-4"
            class="px-2 mx-4" variant="elevated" @click="step--">Tillbaka</v-btn>
          <v-spacer></v-spacer>
          <v-btn v-if="step < 4" size="large" append-icon="mdi-arrow-right-bold" color="light-blue-accent-4"
            class="px-2 mx-4" variant="elevated" @click="step++">Nästa</v-btn>
        </v-card-actions>
      </v-card>
    </v-container>
  </div>
</template>

<script setup>
import Form from "../components/Form.vue";
import FormApply from "../components/FormApply.vue";
import FormSummary from "../components/FormSummary.vue";
import FormDone from "../components/FormDone.vue";
import { reactive, watchEffect, ref } from "vue";
import axios from "axios";
import router from "@/router";

const formData = reactive({
  firstname: "John",
  lastname: "Doe",
  ssn: "12456-1234",
  email: "",
  phoneNumber: "",
  apply: "",
  applyCounty: "",
  applyNumber: "",
});

const formDataApply = reactive({
  areal: false,
  productionType: false,
  averageHensOlderThan20WeeksThisYear: 0,
  averageChickensSlaughteredThisYear: 0,
  averageEggProducingChickensThisYear: 0,

  averageTurkeysOlderThan24WeeksThisYear: 0,
  averageTurkeysSlaughteredThisYear: 0,
  averageEggProducingTurkeysThisYear: 0,
  totalHens: 0,
  totalTurkeys: 0,
  productPlaceFields: [],
});

const step = ref(1);

const responseData = ref(null);

const items = reactive([
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
]);

function updateDisabled() {
  items.forEach((item, index) => {
    item.disabled = index !== step.value - 1;
  });
}

watchEffect(updateDisabled);

async function submitForm() {
  const data = { FormData: formData, FormApply: formDataApply };

  formDataApply.totalHens =
    formDataApply.averageHensOlderThan20WeeksThisYear +
    formDataApply.averageChickensSlaughteredThisYear +
    formDataApply.averageEggProducingChickensThisYear;

  formDataApply.totalTurkeys =
    formDataApply.averageTurkeysOlderThan24WeeksThisYear +
    formDataApply.averageTurkeysSlaughteredThisYear +
    formDataApply.averageEggProducingTurkeysThisYear;

  formDataApply.productPlaceFields;
  console.log(formData);
  console.log(formDataApply);
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

    responseData.value = response.data;

    console.log(response.data);
    console.log(responseData.value);
    document.forms[0].reset();
    step.value = 4;
  } catch (error) {
    console.log(error);
  }
}
</script>

<style></style>
