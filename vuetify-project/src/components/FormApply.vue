<template>
    <form>
        <h2>Produktion</h2>
    <div>
        <v-list-item-group>
            <v-checkbox label="Jag söker krisstöd för min får- och getproduktion"
            color="success"
            />
            <v-checkbox label="Jag söker krisstöd för min fjäderfäproduktion"
            color="success"
            />
            <v-checkbox label="Jag söker krisstöd för min grisproduktion" 
            color="success"
            />
        </v-list-item-group>
    </div>
    <v-text-field type="number" label="Antal får"></v-text-field>
    <v-text-field type="number" label="Antal getter"></v-text-field>

    <div>
        <h2>Ange produktionsplatsnummer för din får- och getproduktion*</h2>
        <v-textarea
          outlined
          value="Ange den/de produktionsplatser där du bedrev din produktion 2018. Varje nummer består av upp till 6 siffror"
        ></v-textarea>
        <v-text-field type="text" prepend-inner-icon="mdi-alpha-s-box" placeholder="XXXX" />
        <v-btn 
        prepend-icon="mdi-plus"
        color="success"
        >
            Lägg till ytterligare produktionsplats
        </v-btn>
        <v-btn 
        prepend-icon="mdi-delete"
        color="red"
        block
        min-width="0"
        >
        Rensa
    </v-btn>
    </div>
</form>
</template>

<script>
</script>

<style scoped>
.v-text-field {
 width: 50%;
}
</style>