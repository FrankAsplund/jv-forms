<template>
    <v-container>
    <form>
        <div class="mt-2 mb-8">
            <h2>Produktion</h2>
        </div>

            <div>
                <v-list-item-group>
                    <v-hover v-slot="{ isHovering, props }">
                        <v-card class="w-75 h-75 my-4" v-bind="props"
                            :color="isHovering ? 'light-green-lighten-5' : undefined">
                            <v-checkbox v-model="productionType" label="Jag söker krisstöd för min fjäderfäproduktion"
                                color="success" hide-details="" />
                        </v-card>
                    </v-hover>
                </v-list-item-group>
            </div>

            <v-container v-if="productionType">
                    <v-container>
                        <v-checkbox label="Hönsproduktion" color="success" v-model="showHens" hide-details />
                        <v-card class="w-100 h-75 my-4" v-if="showHens">
                            <v-text-field name="" v-model="field1" type="text"
                                label="Ange genomsnittlig antal höns äldre än 20 veckor i din besättning 2023"
                                prepend-icon="mdi-plus"></v-text-field>

                            <v-text-field name="" v-model="field2" type="text"
                                label="Ange antal slaktkycklingar i en normal uppfödningsomgång under år 2023"
                                prepend-icon="mdi-plus"></v-text-field>

                            <v-text-field name="" v-model="field3" type="text"
                                label="Ange genomsnittligt antal kycklingar för äggproduktion i din besättning 2023"
                                prepend-icon="mdi-plus"></v-text-field>

                            <v-text-field name="" label="Total summa" v-model="totalHens" readonly
                                prepend-icon="mdi-equal"></v-text-field>
                        </v-card>
                    </v-container>
            </v-container>

            <v-container v-if="productionType">
                    <v-container>
                        <v-checkbox label="Kalkonproduktion" color="success" v-model="showTurkeys" hide-details />
                        <v-card class="w-100 h-75 my-4" v-if="showTurkeys">
                            <v-text-field name="" v-model="field4"
                                label="Ange genomsnittligt antal kalkoner över 24 veckor i din besättning 2023"
                                prepend-inner-icon="mdi-plus-box"></v-text-field>

                            <v-text-field name="" v-model="field5"
                                label="Ange antal slaktkalkoner i en normal uppfödningsomgång under år 2023"
                                prepend-inner-icon="mdi-plus-box"></v-text-field>

                            <v-text-field name="" v-model="field6"
                                label="Ange genomsnittligt antal kalkonkycklingar för äggproduktion i din besättning 2023"
                                prepend-inner-icon="mdi-plus-box"></v-text-field>

                            <v-text-field name="" label="Total summa" v-model="totalTurkeys" readonly
                                prepend-inner-icon="mdi-pound-box">
                            </v-text-field>
                        </v-card>
                    </v-container>
            </v-container>

            <v-container>
                <div class="text-subtitle-1">
                    Om du har dina kalkoner i en kommersiell verksamhet måste du ange produktionsplats.
                </div>
                <v-text-field label="Produktionsplatsnummer"></v-text-field>
                <v-btn prepend-icon="mdi-plus" color="success" class="my-4">
                    Lägg till ytterligare produktionsplats
                </v-btn>
                <v-btn @click="addProductionPlaceNumber" prepend-icon="mdi-delete" color="red" block min-width="0">
                    Rensa
                </v-btn>
            </v-container>
        </v-form>
    </v-container>
</template>

<script>
export default {
    data() {
        return {
            productionType: false,
            showHens: false,
            field1: null,
            field2: null,
            field3: null,
            showTurkeys: false,
            field4: null,
            field5: null,
            field6: null,
        }
    },
    computed: {
        totalHens: function () {
            return Number(this.field1) + Number(this.field2) + Number(this.field3)
        },
        totalTurkeys: function () {
            return Number(this.field4) + Number(this.field5) + Number(this.field6)
        }
    },
    methods: {
        addProductionPlaceNumber() {

        }
    }
}
</script>

<style scoped>
v-list-item-group .v-input__details {
    display: none !important;
}

div.v-container {
    padding: 0;
}
</style>