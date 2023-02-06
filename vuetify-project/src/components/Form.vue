<template>
    <v-container>
        <div class="d-flex justify-center my-2">
            <h1 class="label">Fyll i formuläret</h1>
        </div>

        <div class="d-flex justify-center my-2">
            <p class="label">Backgrundsfärgen har inte blivit bestämd än</p>
        </div>

    <form>
        <v-container class="pa-2 rounded-sm align-items">
            <v-container fluid>
                <v-row variant="outlined">

                    <v-container>
                    <v-col cols="6" md="12" variant="outlined">
                        <h3 class="label">Förnamn<span class="required"> *</span></h3>
                        <v-text-field placeholder="Sofia" type="text" prepend-inner-icon="mdi-account-box"></v-text-field>

                        <h3 class="label">Efternamn<span class="required"> *</span></h3>
                        <v-text-field label="Lundgren" type="text"
                            prepend-inner-icon="mdi-account-box"></v-text-field>
                    </v-col>

                    <v-col cols="12" md="6">
                        <h3 class="label">Personnummer<span class="required"> *</span></h3>
                        <v-text-field label="YYYY-MM-DD-XXXX" type="number"
                        prepend-inner-icon="mdi-account-box"></v-text-field>
                    </v-col>
                        
                        <v-col cols="6" md="12">

                        <h3 class="label">E-post<span class="required"> *</span></h3>
                        <v-text-field label="sofialundgren@epost.se" type="email" prepend-inner-icon="mdi-email"></v-text-field>
                        
                        <h3 class="label">Upprepa E-post<span class="required"> *</span></h3>
                        <v-text-field label="sofialundgren@epost.se" type="email" prepend-inner-icon="mdi-email"></v-text-field>
                    </v-col>
                </v-container>
                </v-row>

                <v-row variant="tonal" class="pa-2">
                    <v-col>
                    <h3 class="label">Söker du som privatperson/enskild firma eller som ombud?<span class="required">*</span></h3>
                    <v-select prepend-inner-icon="mdi-form-select" placeholder="Privatperson">
                    </v-select>

                    <v-container class="pa-0">
                        <h3 class="label">Ange stödmottagarens uppgifter</h3>
                        <v-text-field type="text" label="Organisationsnummer*"
                            append-inner-icon="mdi-help-box"></v-text-field>

                        <v-text-field type="text" label="Företagets/Organisationens namn*"
                            append-inner-icon="mdi-help-box"></v-text-field>
                        </v-container>
                        <!-- INFOBOX -->
                        <!-- INFOBOX -->
                    </v-col>
                    </v-row>
                    <v-container class="my-2">

                    <h3 class="label">Kundnummer</h3>

                    <h5 class="label">Länsbokstav<span class="required"> *</span></h5>
                    <v-text-field type="text" label="Välj i listan"></v-text-field>

                    <h5 class="label">Nummer<span class="required"> *</span></h5>
                    <v-text-field type="text" label="XXXXXX" prepend-inner-icon="mdi-pound-box"
                        append-inner-icon="mdi-help-box"></v-text-field>
                    </v-container>
            </v-container>
        </v-container>
    </form>
</v-container>
</template>

<script>
</script>

<style>
.required {
    font-size: medium;
    color: red;
}

/* .section-2 {
    background-color: rgba(237, 234, 234, 0.855);
    margin-bottom: 50px;
    margin-top: 50px;
} */

form {
    max-width: 80%;
    background: white;
    margin: 30px auto;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}

.label {
    margin-bottom: 4px;
    font-family: 'Poppins', sans-serif;
    
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