<template>
    <v-container>
        <div class="d-flex justify-center my-2">
            <h1 class="label">Ansökan</h1>
        </div>
    <form>
        <div class="mt-2 mb-8">
            <h2>Produktion</h2>
        </div>

        <div>
            <v-list-item-group>
                    <v-hover v-slot="{ isHovering, props }">

                    <v-card class="w-75 h-75 my-4" v-bind="props"
                        :color="isHovering ? 'light-green-lighten-5' : undefined">

                        <v-checkbox label="Jag söker krisstöd för min får- och getproduktion" color="success" />
                    </v-card>
                </v-hover>

                <v-hover v-slot="{ isHovering, props }">
                    <v-card class="w-75 h-75 my-4" v-bind="props"
                    :color="isHovering ? 'light-green-lighten-5' : undefined">
                    <v-checkbox label="Jag söker krisstöd för min fjäderfäproduktion" color="success" />
                </v-card>
            </v-hover>

            <v-hover v-slot="{ isHovering, props }">
                <v-card class="w-75 h-75 my-4" v-bind="props"
                :color="isHovering ? 'light-green-lighten-5' : undefined">
                <v-checkbox label="Jag söker krisstöd för min grisproduktion" color="success" />
            </v-card>
        </v-hover>
                </v-list-item-group>
           
        </div>
        <v-container>
            <v-text-field type="number" class="w-25" label="Antal får"></v-text-field>
            <v-text-field type="number" class="w-25" label="Antal getter"></v-text-field>
        </v-container>
        <div>
            <h2 class="my-4">Ange produktionsplatsnummer för din får- och getproduktion
                <span class="required"> *</span>
            </h2>
            <v-textarea outlined
                value="Ange den/de produktionsplatser där du bedrev din produktion 2018. Varje nummer består av upp till 6 siffror"></v-textarea>
            <v-text-field type="text" prepend-inner-icon="mdi-alpha-s-box" placeholder="XXXX" class="w-50" />
            <v-btn prepend-icon="mdi-plus" color="success" class="my-4">
                Lägg till ytterligare produktionsplats
            </v-btn>
            <v-btn prepend-icon="mdi-delete" color="red" block min-width="0">
                Rensa
            </v-btn>
        </div>
    </form>
</v-container>
</template>

<script>
</script>

<style>
v-list-item-group .v-input__details {
    display: none !important;
}

.required {
    font-size: medium;
    color: red;
}
</style>