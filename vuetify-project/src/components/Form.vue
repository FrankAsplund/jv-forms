<template>
<v-form validate-on="submit">
    <v-container class="pa-2 rounded-sm align-items">
        <c-body body="Ange dina uppgifter" />
        <v-row variant="outlined">
            <v-col cols="12" md="12" variant="outlined">
                <v-text-field label="Förnamn" type="text" prepend-inner-icon="mdi-account-box" :rules="[v => !!v || 'Förnamn måste fyllas i']"></v-text-field>
                <v-text-field label="Efternamn" type="text" prepend-inner-icon="mdi-account-box" :rules="[v => !!v || 'Efternamn måste fyllas i']"></v-text-field>
            </v-col>
            <v-col cols="12" md="6">
                <v-text-field label="Personnummer" type="text" prepend-inner-icon="mdi-account-box" :rules="[v => !!v || 'Personnummer måste fyllas i']" hint="Personnummer måste anges enligt följande format: YYYY-MM-DD-XXXX."></v-text-field>
            </v-col>
            <v-col cols="12" md="12">
                <v-text-field label="E-post" type="email" prepend-inner-icon="mdi-email" :rules="[v => !!v || 'E-post måste fyllas i']"></v-text-field>
                <v-text-field label="Upprepa E-post" type="email" prepend-inner-icon="mdi-email"></v-text-field>
            </v-col>
        </v-row>
        <v-row variant="tonal" class="pa-2">
            <v-col>
                <c-body body="Söker du som privatperson/enskild firma eller som ombud?" />
                <v-select prepend-inner-icon="mdi-form-select" placeholder="Privatperson"></v-select>

    <v-container class="pa-0">
                <c-body body="Ange stödmottagarens uppgifter" />
                    <v-text-field type="text" placeholder="XXXXXX-XXXX" label="Organisationsnummer" hint="Ange stödmottagarens 10-siffriga organisationsnummer enligt följande format: XXXXXX-XXXX. Var noga med att organisationsnumret är kopplat till det kundnummer du anger i ansökan." ></v-text-field>
                    <v-text-field type="text" label="Företagets/Organisationens namn" append-inner-icon="mdi-domain" hint="Ange stödmottagarens företags- eller organisationsnamn."></v-text-field>
            </v-container>
        </v-col>
    </v-row>
    <v-container class="my-2">
        <c-body body="Kundnummer" />
        <v-select label="Länsbokstav" item-title="name" :items="items" prepend-inner-icon="mdi-format-letter-case" return-object></v-select>
        <v-text-field type="text" label="Nummer" placeholder="XXXXXX" prepend-inner-icon="mdi-pound-box" hint="Ange de upp till 6 siffror som tillsammans med länsbokstaven utgör stödmottagarens kundnummer. Observera att kundnummer INTE är samma som produktionsplatsnummer (SE-nr)."></v-text-field>
    </v-container>
</v-container>
</v-form>
</template>

<script setup>
  import cHeader from "./form-components/c-header.vue"
  import cBody from "./form-components/c-body.vue"
  import items from "./form-components/counties.js"
</script>

<script>
export default {
    components: {
        cHeader: cHeader,
        cBody: cBody
    },
    data() {
        return {
            show: false,
            items: items
        };
    }
}
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
    font-family: 'Poppins', sans-serif;
}
</style>