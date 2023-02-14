<template>
  <v-form validate-on="submit" @submit.prevent="submitForm">
    <v-container class="pa-2 rounded-sm align-items">
      <c-body body="Ange dina uppgifter" />
      <v-row variant="outlined">
        <v-col cols="12" md="12" variant="outlined">
          <v-text-field
            label="Förnamn"
            type="text"
            prepend-inner-icon="mdi-account-box"
            :rules="[(v) => !!v || 'Förnamn måste fyllas i']"
            v-model="formData.firstname"
          ></v-text-field>
          <v-text-field
            label="Efternamn"
            type="text"
            prepend-inner-icon="mdi-account-box"
            :rules="[(v) => !!v || 'Efternamn måste fyllas i']"
            v-model="formData.lastname"
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="6">
          <v-text-field
            label="Personnummer"
            type="text"
            prepend-inner-icon="mdi-account-box"
            :rules="[(v) => !!v || 'Personnummer måste fyllas i']"
            hint="Personnummer måste anges enligt följande format: YYYY-MM-DD-XXXX."
            v-model="formData.ssn"
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="12">
          <v-text-field
            label="E-post"
            type="email"
            prepend-inner-icon="mdi-email"
            :rules="[(v) => !!v || 'E-post måste fyllas i']"
            v-model="formData.email"
          ></v-text-field>
          <v-text-field
            label="Upprepa E-post"
            type="email"
            prepend-inner-icon="mdi-email"
          ></v-text-field>
        </v-col>
      </v-row>
      <v-row variant="tonal" class="pa-2">
        <v-col>
          <c-body
            body="Söker du som privatperson/enskild firma eller som ombud?"
          />
          <v-select
            prepend-inner-icon="mdi-form-select"
            placeholder="Jag söker som..."
            :items="applyChoice"
            v-model="formData.apply"
          ></v-select>
        </v-col>
      </v-row>
      <v-container
        v-if="formData.apply === 'Jag söker som privatperson/enskild firma'"
      >
        <v-container class="my-2">
          <c-body body="Kundnummer" />
          <v-select
            label="Länsbokstav"
            item-title="name"
            :items="items"
            prepend-inner-icon="mdi-format-letter-case"
            return-object
            v-model="formData.applyCounty"
          ></v-select>
          <v-text-field
            type="text"
            label="Nummer"
            placeholder="XXXXXX"
            prepend-inner-icon="mdi-pound-box"
            hint="Ange de upp till 6 siffror som tillsammans med länsbokstaven utgör stödmottagarens kundnummer. Observera att kundnummer INTE är samma som produktionsplatsnummer (SE-nr)."
            v-model="formData.applyNumber"
          ></v-text-field>
        </v-container>
      </v-container>

      <v-container class="pa-0">
        <c-body body="Ange stödmottagarens uppgifter" />
        <v-text-field
          type="text"
          placeholder="XXXXXX-XXXX"
          label="Organisationsnummer"
          hint="Ange stödmottagarens 10-siffriga organisationsnummer enligt följande format: XXXXXX-XXXX. Var noga med att organisationsnumret är kopplat till det kundnummer du anger i ansökan."
          v-model="formData.orgnr"
        ></v-text-field>
        <v-text-field
          type="text"
          label="Företagets/Organisationens namn"
          append-inner-icon="mdi-domain"
          hint="Ange stödmottagarens företags- eller organisationsnamn."
          v-model="formData.orgname"
        ></v-text-field>
      </v-container>
    </v-container>

    <v-container class="d-flex justify-center mx-2">
      <v-btn
        type="submit"
        size="large"
        color="success"
        width="200"
        variant="tonal"
        >Submit</v-btn
      >
    </v-container>
  </v-form>

  <v-alert
    v-model="alert"
    v-if="success"
    type="success"
    variant="tonal"
    closable
    close-label="Close Alert"
  >
    {{ response }}
  </v-alert>
  <v-alert v-if="error" type="error">
    {{ error }}
  </v-alert>
</template>

<script setup>
import cHeader from "./form-components/c-header.vue";
import cBody from "./form-components/c-body.vue";
import items from "./form-components/counties.js";
import axios from "axios";
</script>

<script>
export default {
  components: {
    cHeader: cHeader,
    cBody: cBody,
  },
  name: "Form",
  data() {
    return {
      show: false,
      items: items,
      applyChoice: [
        "Jag söker som privatperson/enskild firma",
        "Jag söker som ombud för privatperson/enskild firma",
        "Jag söker som ombud för ett företag eller organisation",
      ],

      formData: {
        firstname: "",
        lastname: "",
        ssn: "", // Social Security Number, personnummer på engelska
        email: "",
        apply: "", //Ombud, privatperson osv
        applyCounty: "",
        applyNumber: "",
        orgnr: "",
        orgname: "",
      },
      response: "",
      success: false,
      error: false,
    };
  },

  methods: {
    submitForm() {
      var config = {
        method: "POST",
        url: "https://dummy.restapiexample.com/api/v1/create",
        headers: {
          "Content-Type": "application/json",
        },
        data: JSON.stringify(this.formData),
      };

      axios(config)
        .then((response) => {
          this.response = JSON.stringify(response.data);
          console.log(JSON.stringify(response.data));
          this.success = true;
          this.error = false;
        })
        .catch((error) => {
          console.log(error);
          this.error = error.message;
          this.success = false;
        });
    },
  },
};
</script>

<style>
form {
  max-width: 80%;
  background: white;
  margin: 30px 30px 0px 30px;
  text-align: left;
  padding: 20px;
  border-radius: 10px;
}

.label {
  margin-bottom: 4px;
  font-family: "Poppins", sans-serif;
}
</style>
