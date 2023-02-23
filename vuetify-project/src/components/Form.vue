<template>
  <v-form validate-on="submit">
    <v-container class="pa-2 rounded-sm align-items">
      <c-body body="Ange dina uppgifter" />
      <v-row variant="outlined">
        <v-row variant="outlined" class="ma-2 pa-0">
          <v-text-field label="Förnamn" type="text" model-value="John" prepend-inner-icon="mdi-account-box"
            disabled></v-text-field>
          <v-text-field label="Efternamn" model-value="Doe" type="text" prepend-inner-icon="mdi-account-box"
            disabled></v-text-field>
          <v-text-field label="Personnummer" type="text" model-value="12456-1234" prepend-inner-icon="mdi-account-box"
            disabled></v-text-field>
        </v-row>
        <v-col cols="12" md="12">
          <v-text-field label="E-post" type="email" prepend-inner-icon="mdi-email" v-model="formData.email"
            hint="Skriv in din e-postadress."></v-text-field>
          <v-text-field label="Upprepa E-post" type="email" prepend-inner-icon="mdi-email"
            hint="Skriv in samma e-postadress som ovan."
            ></v-text-field>

          <v-text-field label="Telefonnummer" type="text" v-model="formData.phoneNumber" prepend-inner-icon="mdi-phone"
            :rules="[
              v => !!v || 'Field is required'
            ]"></v-text-field>
        </v-col>
      </v-row>

      <v-row variant="tonal" class="pa-2">
        <v-col>
          <c-body body="Söker du som privatperson/enskild firma eller som ombud?" />
          <v-select prepend-inner-icon="mdi-form-select" placeholder="Jag söker som..." :items="applyChoice"
            v-model="formData.apply" :rules="[
        v => !!v || 'Field is required'
      ]"></v-select>
        </v-col>
      </v-row>
      <v-container v-if="formData.apply === 'Jag söker som privatperson/enskild firma'">
        <v-container class="my-2">
          <c-body body="Kundnummer" />
          <v-select label="Länsbokstav" item-title="name" :items="items" prepend-inner-icon="mdi-format-letter-case"
            return-object v-model="formData.applyCounty"></v-select>
          <v-text-field type="text" label="Nummer" placeholder="XXXXXX" prepend-inner-icon="mdi-pound-box"
            hint="Ange de upp till 6 siffror som tillsammans med länsbokstaven utgör stödmottagarens kundnummer. Observera att kundnummer INTE är samma som produktionsplatsnummer (SE-nr)."
            v-model="formData.applyNumber"></v-text-field>
        </v-container>
      </v-container>
    </v-container>

    <v-container class="d-flex justify-center mx-2">
      <v-btn type="submit" size="large" color="success" width="200" variant="tonal">Submit</v-btn>
    </v-container>
  </v-form>
</template>

<script setup>
import cHeader from "./form-components/c-header.vue";
import cBody from "./form-components/c-body.vue";
import items from "./form-components/counties.js";

const props = defineProps({
  formData: Object,
});
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
     /*  rules: [
        value => {
          if (value) return true
          return 'You must enter an input.'
        },
      ], */
    };
  },
};
</script>

<style>
form {
  max-width: 80%;
  background: white;
  margin: 0px 30px 0px 30px;
  text-align: left;
  padding: 20px;
  border-radius: 10px;
}

.label {
  margin-bottom: 4px;
  font-family: "Poppins", sans-serif;
}
</style>
