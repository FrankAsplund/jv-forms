<template>
  <div class="d-flex bg-indigo-lighten-4 justify-center h-100">
    <v-container class="rounded mx-12 mt-16">
      <v-card class="rounded-t-lg">
        <v-toolbar
          class="bg-indigo-darken-1 text-h5 font-weight-bold justify-center elevation-4"
          dark
        >
          <v-breadcrumbs class="pa-4" :items="items" mobile-breakpoint="580">
            <template #title="{ item }">
              {{ item.title }}
            </template>
          </v-breadcrumbs>
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
            size="x-large"
            icon="mdi:mdi-arrow-right-bold"
            color="black"
            @click="step++"
          ></v-btn>
        </v-card-actions>

        <v-window v-model="step" class="mx-6">
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
import axios from "axios";

import { onMounted } from "vue";
import { useDisplay } from "vuetify";

const { width, mobile } = useDisplay();

onMounted(() => {
  console.log(width.value); // 960
  console.log(mobile.value); // true
});

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
  application_check: false,
  application_expand: false,

  application_expand_mental_anxiety_slider: null,
  application_expand_mental_stress_slider: null,
  application_expand_mental_health_slider: null,

  application_expand_mental: false,
  application_expand_physical: false,

  application_expand_physical_health_slider: null,
  application_expand_physical_activity_slider: null,
  application_expand_physical_body_slider: null,
});

const step = ref(1);

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

async function submitForm() {
  loading.value = true;
  const data = { FormData: formData, FormApply: formDataApply };

  formDataApply.application_expand_mental;
  formDataApply.application_expand_physical;

  try {
    axios
      .post("http://localhost:8000/posts", data)
      .then((response) => console.log(response));
    responseData.value = data;

    step.value = 4;
  } catch (error) {
    console.log(error);
  }
  loading.value = false;
}
</script>

<style>
.loading-indicator {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

@media only screen and (max-width: 600px) {
  .v-breadcrumbs {
    display: block !important;
    /* display: flex; */
    align-items: center;
    line-height: 1.375rem;
    /* padding: 16px 12px; */
  }

  .text-h5 {
    font-size: 1.5rem !important;
  }

  .mx-12 {
    margin-right: 0px !important;
    margin-left: 0px !important;
  }
}
</style>
