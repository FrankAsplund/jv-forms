<template>
    <form>
    <v-text-field label="Personnummer*" type="number" prepend-inner-icon="mdi-account-box"></v-text-field>

    <v-text-field label="Förnamn*" type="text" prepend-inner-icon="mdi-account-box"></v-text-field>

    <v-text-field label="Efternamn*" type="text" prepend-inner-icon="mdi-account-box"></v-text-field>

    <v-text-field label="E-post*" type="email" prepend-inner-icon="mdi-email"></v-text-field>

    <v-text-field label="Upprepa E-post*" type="email" prepend-inner-icon="mdi-email"></v-text-field>
    
    <h2>Söker du som privatperson/enskild firma eller som ombud?<span class="requiered">*</span></h2>
    <v-select prepend-inner-icon="mdi-form-select" placeholder="Privatperson">
    </v-select>

    <div class="section-2">
    <h2>Ange stödmottagarens uppgifter</h2>
    <v-text-field type="text" label="Organisationsnummer*" append-inner-icon="mdi-help-box"></v-text-field>

    <v-text-field type="text" label="Företagets/Organisationens namn*" append-inner-icon="mdi-help-box"></v-text-field>
    </div>
    <!-- INFOBOX -->
    <!-- INFOBOX -->

    <h2>Kundnummer</h2>
    <v-text-field type="text" label="Länsbokstav" />
    <v-text-field type="text" label="Nummer*" prepend-inner-icon="mdi-pound-box" append-inner-icon="mdi-help-box" />
</form>
</template>

<script>
</script>

<style>

.requiered {
    font-size: medium;
    color: red;
}
.section-2 {
    background-color: rgba(237, 234, 234, 0.855);
    margin-bottom: 50px;
    margin-top: 50px;
}

form {
  max-width: 80%;
  background: white;
  margin: 30px auto;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}

/* label {
  color: rgb(63, 62, 62);
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
} */

/* input,
select {
  display: inline-block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
  box-shadow: rgba(50, 50, 93, 0.25) 0px 6px 12px -2px,
    rgba(0, 0, 0, 0.3) 0px 3px 7px -3px;
} */
</style>