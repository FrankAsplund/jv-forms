<template>
    <v-container>
        <v-form>
            <div class="mt-2 mb-8">
                <div class="text-h5">Produktion</div>
            </div>

            <div>
                <v-hover v-slot="{ isHovering, props }">
                    <v-card class="w-75 h-75 my-4" v-bind="props" :color="isHovering ? 'light-green-lighten-5' : undefined">
                        <v-checkbox v-model="productionType" label="Jag söker krisstöd för min fjäderfäproduktion"
                            color="success" hide-details />
                    </v-card>
                </v-hover>
            </div>

            <v-container v-if="productionType">
                <v-container>
                    <v-checkbox label="Hönsproduktion" color="success" v-model="showHens" hide-details />
                    <v-card class="w-100 h-75 my-4" v-if="showHens">
                        <v-text-field v-model="field1" type="text"
                            label="Ange genomsnittlig antal höns äldre än 20 veckor i din besättning 2023"
                            prepend-icon="mdi-plus-box"></v-text-field>

                        <v-text-field v-model="field2" type="text"
                            label="Ange antal slaktkycklingar i en normal uppfödningsomgång under år 2023"
                            prepend-icon="mdi-plus-box"></v-text-field>

                        <v-text-field v-model="field3" type="text"
                            label="Ange genomsnittligt antal kycklingar för äggproduktion i din besättning 2023"
                            prepend-icon="mdi-plus-box"></v-text-field>

                        <v-text-field label="Total summa" v-model="totalHens" readonly
                            prepend-icon="mdi-equal-box"></v-text-field>
                    </v-card>
                </v-container>
            </v-container>

            <v-container v-if="productionType">
                <v-container>
                    <v-checkbox label="Kalkonproduktion" color="success" v-model="showTurkeys" hide-details />
                    <v-card class="w-100 h-75 my-4" v-if="showTurkeys">
                        <v-text-field v-model="field4"
                            label="Ange genomsnittligt antal kalkoner över 24 veckor i din besättning 2023"
                            prepend-icon="mdi-plus-box"></v-text-field>

                        <v-text-field v-model="field5"
                            label="Ange antal slaktkalkoner i en normal uppfödningsomgång under år 2023"
                            prepend-icon="mdi-plus-box"></v-text-field>

                        <v-text-field v-model="field6"
                            label="Ange genomsnittligt antal kalkonkycklingar för äggproduktion i din besättning 2023"
                            prepend-icon="mdi-plus-box"></v-text-field>

                        <v-text-field label="Total summa" v-model="totalTurkeys" readonly prepend-icon="mdi-equal-box">
                        </v-text-field>
                    </v-card>
                </v-container>
            </v-container>

            <v-container class="productionplace-container">
                <div class="text-subtitle-1">
                    Om du har dina kalkoner i en kommersiell verksamhet måste du ange produktionsplats.
                </div>
                <v-text-field label="Produktionsplatsnummer" prefix="SE"
                    hint="Ange den/de produktionsplatser där du bedrev din produktion 2023. Varje nummer består av upp till 6 siffor.">
                </v-text-field>
                <v-text-field v-for="(field, index) in productPlaceFields" :key="index" :label="'Produktionsplatsnummer'"
                    prefix="SE" v-model="field.value">
                    <template v-slot:append>
                        <v-icon @click="removeProductionPlace(index)" :style="{ color: 'red' }">mdi-delete</v-icon>
                    </template>
                </v-text-field>
                <v-btn @click="addProductionPlace" prepend-icon="mdi-plus" color="success" class="my-4">
                    Lägg till produktionsplats
                </v-btn>
            </v-container>
        </v-form>
</v-container>
</template>

<script>
import cHeader from "./form-components/c-header.vue";
import cBody from "./form-components/c-body.vue";

export default {
    components: {
        cHeader: cHeader,
        cBody: cBody,
    },
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
            productPlaceFields: [],
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
        addProductionPlace() {
            this.productPlaceFields.push({ value: '' });
        },
        removeProductionPlace(index) {
            this.productPlaceFields.splice(index, 1);
        }
    }
}
</script>

<style scoped>
.productionplace-container {
    margin-top: 5rem;
}

.my-field .v-icon {
    color: red !important;
}
</style>
