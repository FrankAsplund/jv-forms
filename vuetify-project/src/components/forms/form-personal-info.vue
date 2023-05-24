<template>
  <v-form v-if="v$" validate-on="submit" variant="filled">
    <v-container class="pa-2 rounded-sm align-items">
      <custom-body body="Ange dina personliga uppgifter" />
      <div variant="outlined">
        <v-row variant="outlined" class="ma-2 pa-0">
          <v-text-field
            v-model="formData.applicant_firstname"
            class="mx-2"
            label="Förnamn"
            type="text"
            prepend-inner-icon="mdi:mdi-account-box"
          ></v-text-field>
          <v-text-field
            v-model="formData.applicant_lastname"
            class="mx-2"
            label="Efternamn"
            type="text"
            prepend-inner-icon="mdi:mdi-account-box"
          ></v-text-field>
          <v-text-field
            v-model="formData.applicant_personal_number"
            class="mx-2"
            label="Personnummer"
            type="text"
            prepend-inner-icon="mdi:mdi-account-box"
          ></v-text-field>
        </v-row>
        <v-col cols="12" md="12">
          <v-text-field
            v-model="v$.contact_email.$model"
            :error-messages="v$.contact_email.$errors[0]?.$message"
            label="E-post"
            type="email"
            prepend-inner-icon="mdi:mdi-email"
            hint="Skriv in din e-postadress."
          ></v-text-field>
          <v-text-field
            v-model="v$.confirmContactEmail.$model"
            :error-messages="
              v$.confirmContactEmail.$errors.map((err) => err.$message)
            "
            label="Upprepa E-post"
            type="email"
            prepend-inner-icon="mdi:mdi-email"
            hint="Skriv in samma e-postadress som ovan."
          ></v-text-field>

          <v-text-field
            v-model="v$.applicant_customer_number.$model"
            :error-messages="v$.applicant_customer_number.$errors[0]?.$message"
            :hide-details="false"
            label="Telefonnummer"
            type="text"
            prepend-inner-icon="mdi:mdi-phone"
          ></v-text-field>
        </v-col>
      </div>

      <v-row variant="tonal" class="pa-2">
        <v-col>
          <custom-body body="Vilket län bor du i?" />
          <v-select
            label="Län"
            v-model="v$.applicant_type.$model"
            :error-messages="v$.applicant_type.$errors[0]?.$message"
            prepend-inner-icon="mdi:mdi-form-select"
            item-title="place"
            :items="items"
            return-object
          ></v-select>
        </v-col>
      </v-row>
    </v-container>
  </v-form>
</template>

<script setup>
import CustomBody from "../form-components/c-body.vue";
import items from "../form-components/counties.js";
import { useVModels } from "@vueuse/core";
import { reactive, computed, watchEffect } from "vue";

import { useVuelidate } from "@vuelidate/core";
import {
  required,
  email,
  sameAs,
  helpers,
  requiredIf,
  numeric,
} from "@vuelidate/validators";

const props = defineProps({
  formDataObj: {
    type: Object,
    default: () => ({
      applicant_firstname: "",
      applicant_lastname: "",
      applicant_personal_number: "",
      contact_email: "",
      confirmContactEmail: "",
      applicant_customer_number: "",
      applicant_type: "",
      applicant_county_name: "",
      applicant_county: "",
    }),
  },
  valid: {
    type: Boolean,
    default: false,
  },
});

const emit = defineEmits([
  "update:modelValue",
  "update:formDataObj",
  "update:valid",
]);
const { formDataObj: formData, valid: isFormValid } = useVModels(props, emit);

const rules = computed(() => {
  return {
    //applicant_lastname: { required },
    contact_email: {
      required: helpers.withMessage("Fältet är tomt.", required),
      email: helpers.withMessage("Ange en korrekt e-post", email),
    },
    confirmContactEmail: {
      required: helpers.withMessage("Fältet är tomt.", required),
      sameAs: helpers.withMessage(
        "E-posten måste matcha ovan",
        sameAs(formData.value.contact_email)
      ),
    },
    applicant_customer_number: {
      required: helpers.withMessage("Fältet är tomt.", required),
      numeric: helpers.withMessage(
        "Enbart siffror är tillåtet i detta fält",
        numeric
      ),
    },
    applicant_type: { required },
    applicant_county_name: {
      requiredIfRef: requiredIf(
        formData.value.applicant_type ===
          "Jag söker som privatperson/enskild firma"
      ),
    },
    applicant_county: {
      requiredIfRef: helpers.withMessage(
        "Ange kundnummer.",
        requiredIf(
          formData.value.applicant_type ===
            "Jag söker som privatperson/enskild firma"
        )
      ),
    },
  };
});

const v$ = useVuelidate(rules, formData.value);

watchEffect(() => {
  isFormValid.value = !v$.value.$invalid;
});
</script>

<style>
form {
  max-width: 100%;
  background: white;
  text-align: left;
  border-radius: 10px;
}

.label {
  margin-bottom: 4px;
  font-family: "Poppins", sans-serif;
}
</style>
