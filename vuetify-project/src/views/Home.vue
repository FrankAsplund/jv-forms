<template>
  <div class="d-flex bg-light-green-lighten-4 justify-center h-100">
    <v-container class="rounded mx-12">
      <v-card class="rounded-t-lg">
        <v-toolbar
          class="bg-light-blue-lighten-5 text-h5 font-weight-bold justify-center elevation-4"
          dark
        >
          <v-breadcrumbs :items="items">
            <template #title="{ item }">
              {{ item.title }}
            </template>
          </v-breadcrumbs>
          <v-toolbar-title class="text-h5 font-weight-bold"></v-toolbar-title>
        </v-toolbar>

        <v-card-actions>
          <v-btn
            v-if="step > 1 && step < 4"
            size="x-large"
            icon="mdi:mdi-arrow-left-bold"
            color="black"
            @click="step--"
          ></v-btn>
          <v-spacer></v-spacer>
          <v-btn
            v-if="step < 3"
            :disabled="!canGoNext"
            size="x-large"
            icon="mdi:mdi-arrow-right-bold"
            color="black"
            @click="step++"
          ></v-btn>
        </v-card-actions>

        <v-window v-model="step" class="mx-12">
          <v-defaults-provider :defaults="jvDefaults">
            <v-window-item :value="1">
              <personal-info-form
                v-model:formDataObj="formData"
                v-model:valid="isPersonalInfoFormValid"
              />
            </v-window-item>

            <v-window-item :value="2">
              <application-form
                v-model:formDataApplyObj="formDataApply"
                v-model:valid="isApplyFormValid"
                v-model:selected-files="selectedFiles"
              />
            </v-window-item>

            <v-window-item :value="3">
              <summary-form
                v-model:valid="isSummaryFormValid"
                v-model:step-prop="step"
                :form-data="formData"
                :form-data-apply="formDataApply"
                @submit-all="submitForm()"
              />
            </v-window-item>
            <v-window-item :value="4">
              <done-form :response-data="responseData" />
            </v-window-item>
          </v-defaults-provider>
        </v-window>
        <v-card-actions>
          <v-btn
            v-if="step > 1 && step < 4"
            size="large"
            prepend-icon="mdi:mdi-arrow-left-bold"
            color="light-blue-accent-4"
            class="px-2 mx-4"
            variant="elevated"
            @click="step--"
          >
            Tillbaka
          </v-btn>
          <v-spacer></v-spacer>
          <v-btn
            v-if="step < 3"
            :disabled="!canGoNext"
            size="large"
            append-icon="mdi:mdi-arrow-right-bold"
            color="light-blue-accent-4"
            class="px-2 mx-4"
            variant="elevated"
            @click="step++"
          >
            Nästa
          </v-btn>
        </v-card-actions>
      </v-card>
      <div v-if="loading">
        <v-progress-circular
          class="loading-indicator"
          indeterminate
          color="blue"
          size="128"
        ></v-progress-circular>
      </div>
    </v-container>
  </div>
</template>

<script setup>
import PersonalInfoForm from "../components/forms/form-personal-info.vue";
import ApplicationForm from "../components/forms/form-application.vue";
import SummaryForm from "../components/forms/form-summary.vue";
import DoneForm from "../components/forms/form-done.vue";
import { reactive, watchEffect, ref, watch, computed } from "vue";
/* import { useOnifyApi } from "@onify/helix-core"; */

// import { useOnifyApi } from '@onify/helix-core';
// const onifyHttpRequest = useOnifyApi();

/* const onifyApiRequest = useOnifyApi(); */

const loading = ref(false);

const formData = reactive({
  applicant_firstname: "",
  applicant_lastname: "",
  applicant_personal_number: "",
  contact_email: "",
  confirmContactEmail: "",
  applicant_customer_number: "",
  applicant_type: "",
  applicant_county_name: "",
  applicant_county: "",
});

const formDataApply = reactive({
  application_area: false,
  application_poultry: false,
  application_poultry_hens_older: null,
  application_poultry_hens_broilers: null,
  application_poultry_hens_egg: null,

  application_poultry_hens: false,
  application_poultry_turkeys: false,

  application_poultry_turkeys_older: null,
  application_poultry_turkeys_broilers: null,
  application_poultry_turkeys_egg: null,

  application_poultry_hens_total_count: 0,
  application_poultry_turkeys_total_count: 0,

  // Initial value in Product Place fields array
  application_sites_turkeys: [{ value: "" }],
  application_sites_hens: [{ value: "" }],
  attachments: [],
});

const step = ref(1);
const selectedFiles = ref([]);

const isPersonalInfoFormValid = ref(false);
const isApplyFormValid = ref(false);
const isSummaryFormValid = ref(false);

const canGoNext = computed(() => {
  switch (step.value) {
    case 1:
      return isPersonalInfoFormValid.value;
    case 2:
      return isApplyFormValid.value;
    case 3:
      return isSummaryFormValid.value;
    default:
      return true;
  }
});

const responseData = ref({});

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

/* const { data: userSettings } = onifyApiRequest.fetch("/my/settings");
watch(userSettings, () => {
  formData.applicant_firstname = userSettings.value?.custom?.firstname;
  formData.applicant_lastname = userSettings.value?.custom?.lastname;
  formData.applicant_personal_number =
    userSettings.value?.custom?.personal_number;
}); */

function upload() {
  try {
    // Remove this when implementing onifyApiRequest
    /* const apiUrl = "/files/public/"; */

    return selectedFiles.value.map(async (file) => {
      return new Promise((resolve, reject) => {
        try {
          const fileReader = new FileReader();

          fileReader.onload = async (e) => {
            const arrayBuffer = e.target.result;

            const response = await onifyApiRequest.update(apiUrl + file.name, {
              body: arrayBuffer,
            });
            console.log("File upload successful:", response);

            // Convert the response object to JSON
            const jsonResponse = await response.json();

            // Delete the 'content' property from the jsonResponse object
            delete jsonResponse.content;

            // Push the modified jsonResponse object to the formDataApply.attachments array
            formDataApply.attachments.push(jsonResponse);

            resolve();
          };

          fileReader.onerror = (error) => {
            console.error("Error reading file:", error);
          };

          fileReader.readAsArrayBuffer(file);
        } catch (error) {
          console.error("Error uploading file:", error);
          reject();
        }
      });
    });
  } catch (error) {
    console.error("Error uploading files:", error);
  }
}

async function submitForm() {
  loading.value = true;
  const data = { FormData: formData, FormApply: formDataApply };

  formDataApply.application_poultry_hens_total_count =
    formDataApply.application_poultry_hens_older +
    formDataApply.application_poultry_hens_broilers +
    formDataApply.application_poultry_hens_egg;

  formDataApply.application_poultry_turkeys_total_count =
    formDataApply.application_poultry_turkeys_older +
    formDataApply.application_poultry_turkeys_broilers +
    formDataApply.application_poultry_turkeys_egg;

  formDataApply.application_sites_turkeys;
  formDataApply.application_sites_hens;

  await Promise.all(upload());

  try {
    const response = await onifyApiRequest.update(
      "/my/workflows/run/create-case",
      { json: data }
    );

    responseData.value = (await response.json()).output;
    console.log(responseData.value);

    step.value = 4;
  } catch (error) {
    console.log(error);
  }
  loading.value = false;
}
</script>

<style>
/* Temporary styling */
.basic-layout-body {
  display: flex;
  padding: 0;
  width: 100%;
}

.loading-indicator {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>
