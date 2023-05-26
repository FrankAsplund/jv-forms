<template>
  <v-form>
    <div class="text-h3">Summering</div>
    <div class="line-divider"></div>

    <div class="summary-info">
      <div class="text-body-2">
        Här har du möjlighet att granska, gå tillbaka och ändra.
        <br />
        Du kan hoppa till valfritt avsnitt genom att klicka på önskad sida i
        listan ovan. Ändra uppgift och klicka sedan på denna sida i listan igen
      </div>
    </div>

    <v-container class="mb-2">
      <v-container class="elevation-2 pa-2 mb-2">
        <custom-body body="Grunduppgifter" />

        <v-table density="compact">
          <thead>
            <tr>
              <th class="text-left">Förnamn</th>
              <th class="text-right">{{ formData.applicant_firstname }}</th>
            </tr>
            <tr>
              <th class="text-left">Efternamn</th>
              <th class="text-right">{{ formData.applicant_lastname }}</th>
            </tr>
            <tr>
              <th class="text-left">Personnummer</th>
              <th class="text-right">
                {{ formData.applicant_personal_number }}
              </th>
            </tr>
            <tr>
              <th class="text-left">Epost-address</th>
              <th class="text-right">{{ formData.contact_email }}</th>
            </tr>
            <tr>
              <th class="text-left">Telefonnummer</th>
              <th class="text-right">
                {{ formData.applicant_customer_number }}
              </th>
            </tr>
            <tr>
              <th class="text-left">Län</th>
              <th class="text-right">{{ formData.applicant_type }}</th>
            </tr>
          </thead>
        </v-table>
        <!-- <div class="justify-center pa-2"> -->
        <v-btn
          @click="stepBack_personal_info_form"
          class="justify-center pa-2 my-2"
          color="success"
          >Ändra uppgifter</v-btn
        >
        <!-- </div> -->
      </v-container>

      <v-container class="elevation-2 pa-2 mb-2">
        <custom-body body="Undersökning" />
        <!-- <div class="text-caption"></div> -->
        <v-table density="compact">
          <thead>
            <tr>
              <th class="text-left">
                Jag mår fysiskt och mentalt bra de flesta dagarna
              </th>
              <th class="text-right">
                {{ formDataApply.application_check ? "Ja" : "Nej" }}
              </th>
            </tr>
            <tr>
              <th class="text-left">
                Jag är villig att besvara ytterligare frågor om min hälsa
              </th>
              <th class="text-right">
                {{ formDataApply.application_expand ? "Ja" : "Nej" }}
              </th>
            </tr>
          </thead>
          <v-btn
            @click="stepBack_application_form"
            class="justify-center pa-2 my-2"
            color="success"
            >Ändra uppgifter</v-btn
          >
        </v-table>
      </v-container>

      <v-card
        variant="elevated"
        class="elevation-4 justify-center w-100 h-50 my-4"
      >
        <custom-body class="pa-2" body="Godkännande och försäkran" />
        <v-checkbox
          class="text-high-emphasis font-weight-regular pa-2"
          v-model="summaryCheckbox"
          color="success"
        >
          <template #label>
            <div>
              Jag intygar att:
              <br />

              Jag är införstådd med och uppfyller de villkor som finns för att
              få ta del av undersökningen. Jag förstår och går med på att denna
              undersökningen kan användas och granskas av behöriga personer.
            </div>
          </template>
        </v-checkbox>
      </v-card>
      <div v-if="summaryCheckbox" class="send-btn">
        <v-btn color="success" size="large" @click="submit()">Skicka in</v-btn>
      </div>
    </v-container>
  </v-form>
</template>

<script setup>
import { ref } from "vue";
import { useVModel } from "@vueuse/core";
import CustomBody from "../form-components/c-body.vue";

const props = defineProps({
  formData: {
    type: Object,
    default: null,
  },
  formDataApply: {
    type: Object,
    default: null,
  },
  stepProp: {
    type: Number,
    default: null,
  },
});

function stepBack_personal_info_form() {
  stepProp.value = 1;
}

function stepBack_application_form() {
  stepProp.value--;
}

const summaryCheckbox = ref(false);

const emit = defineEmits([
  "submit-all",
  "update:modelValue",
  "update:stepProp",
]);
const stepProp = useVModel(props, "stepProp", emit);

const submit = () => {
  emit("submit-all");
};
</script>

<style scoped>
.send-btn {
  text-align: center;
  /* padding: 10px; */
}

/* .summary-btn {
  text-align: center;
  padding: 10px;
} */

/* .summaryConfirmContainer {
  margin: auto;
  width: 70%;
  box-shadow: rgba(60, 64, 67, 0.3) 0px 1px 2px 0px,
    rgba(60, 64, 67, 0.15) 0px 1px 3px 1px;
  padding: 10px;
  margin-bottom: 0.5rem;
} */

/* .flex-container {
  display: flex;
  margin-bottom: 2rem;
  width: 100%;
} */

.line-divider {
  margin-top: 1.5rem;
  margin-bottom: 0.5rem;
  border-bottom: 2px solid rgb(156, 207, 111);
}

.summary-info {
  margin-bottom: 1.5rem;
}

@media only screen and (max-width: 600px) {
  .flex-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  /* .confirmCard {
    display: grid !important;
    width: 90% !important;
  } */
}
</style>
