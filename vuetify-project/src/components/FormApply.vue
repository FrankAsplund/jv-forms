<template>
  <v-form validate-on="submit">
    <v-container class="pa-2 rounded-sm align-items">
      <c-body body="Produktion" />
      <v-hover v-slot="{ isHovering, props }">
        <v-card class="w-75 h-75 my-4" v-bind="props" :color="isHovering ? 'light-green-lighten-5' : undefined">
          <v-checkbox v-model="formDataApply.productionType" label="Jag söker krisstöd för min fjäderfäproduktion"
            color="success" hide-details />
        </v-card>
      </v-hover>

      <v-hover v-slot="{ isHovering, props }">
        <v-card class="w-75 h-75 my-4" v-bind="props" :color="isHovering ? 'light-green-lighten-5' : undefined">
          <v-checkbox v-model="formDataApply.areal" label="Jag söker krisstöd för areal" color="success" hide-details />
        </v-card>
      </v-hover>

      <v-container v-if="formDataApply.productionType">
        <v-container>
          <v-checkbox label="Hönsproduktion" color="success" v-model="showHens" hide-details />
          <v-card class="w-100 h-75 my-4" v-if="showHens">
            <v-text-field v-model.number="formDataApply.averageHensOlderThan20WeeksThisYear" type="number"
              label="Ange genomsnittlig antal höns äldre än 20 veckor i din besättning 2023"
              prepend-icon="mdi-plus-box"></v-text-field>

            <v-text-field v-model.number="formDataApply.averageChickensSlaughteredThisYear" type="number"
              label="Ange antal slaktkycklingar i en normal uppfödningsomgång under år 2023"
              prepend-icon="mdi-plus-box"></v-text-field>

            <v-text-field v-model.number="formDataApply.averageEggProducingChickensThisYear" type="number"
              label="Ange genomsnittligt antal kycklingar för äggproduktion i din besättning 2023"
              prepend-icon="mdi-plus-box"></v-text-field>

            <v-text-field label="Total summa" v-model="totalHens" readonly prepend-icon="mdi-equal-box"></v-text-field>
          </v-card>
        </v-container>
      </v-container>

      <v-container v-if="formDataApply.productionType">
        <v-container>
          <v-checkbox label="Kalkonproduktion" color="success" v-model="showTurkeys" hide-details />
          <v-card class="w-100 h-75 my-4" v-if="showTurkeys">
            <v-text-field v-model.number="formDataApply.averageTurkeysOlderThan24WeeksThisYear"
              label="Ange genomsnittligt antal kalkoner över 24 veckor i din besättning 2023"
              prepend-icon="mdi-plus-box"></v-text-field>

            <v-text-field v-model.number="formDataApply.averageTurkeysSlaughteredThisYear"
              label="Ange antal slaktkalkoner i en normal uppfödningsomgång under år 2023"
              prepend-icon="mdi-plus-box"></v-text-field>

            <v-text-field v-model.number="formDataApply.averageEggProducingTurkeysThisYear"
              label="Ange genomsnittligt antal kalkonkycklingar för äggproduktion i din besättning 2023"
              prepend-icon="mdi-plus-box"></v-text-field>

            <v-text-field label="Total summa" v-model="totalTurkeys" readonly prepend-icon="mdi-equal-box"></v-text-field>
          </v-card>
        </v-container>
      </v-container>

      <v-container class="productionplace-container">
        <div class="text-subtitle-1">
          Om du har dina kalkoner i en kommersiell verksamhet måste du ange
          produktionsplats.
        </div>
        <v-text-field label="Produktionsplatsnummer" prefix="SE"
          hint="Ange den/de produktionsplatser där du bedrev din produktion 2023. Varje nummer består av upp till 6 siffor.">
        </v-text-field>
        <v-text-field v-for="(field, index) in formDataApply.productPlaceFields" :key="index"
          :label="'Produktionsplatsnummer'" prefix="SE" v-model="field.value">
          <template v-slot:append>
            <v-icon @click="removeProductionPlace(index)" :style="{ color: 'red' }">mdi-delete</v-icon>
          </template>
        </v-text-field>
        <v-btn @click="addProductionPlace" prepend-icon="mdi-plus" color="success" class="my-4">
          Lägg till produktionsplats
        </v-btn>
      </v-container>

      <v-container class="d-flex justify-center mx-2">
      </v-container>
    </v-container>
  </v-form>
</template>

<script setup>
import cHeader from "./form-components/c-header.vue";
import cBody from "./form-components/c-body.vue";
import { useVModel } from "@vueuse/core";
import { ref, computed } from 'vue'

const showHens = ref(false);
const showTurkeys = ref(false);

const totalHens = computed(
  () =>
  (Number(props.formDataApplyObj.averageHensOlderThan20WeeksThisYear) +
    Number(props.formDataApplyObj.averageChickensSlaughteredThisYear) +
    Number(props.formDataApplyObj.averageEggProducingChickensThisYear))
);

const totalTurkeys = computed(
  () =>
  (Number(props.formDataApplyObj.averageTurkeysOlderThan24WeeksThisYear) +
    Number(props.formDataApplyObj.averageTurkeysSlaughteredThisYear) +
    Number(props.formDataApplyObj.averageEggProducingTurkeysThisYear))
);

const props = defineProps({
  formDataApplyObj: {
    type: Object,
    default: () => ({
      areal: false,
      productionType: false,
      averageHensOlderThan20WeeksThisYear: 0,
      averageChickensSlaughteredThisYear: 0,
      averageEggProducingChickensThisYear: 0,

      averageTurkeysOlderThan24WeeksThisYear: 0,
      averageTurkeysSlaughteredThisYear: 0,
      averageEggProducingTurkeysThisYear: 0,

      productPlaceFields: []
    }),
  },
});

const emit = defineEmits(["update:modelValue", "update:formDataApply"]);
const formDataApply = useVModel(props, "formDataApplyObj", emit);

function addProductionPlace() {
  formDataApply.value.productPlaceFields.push({ value: "" });
};

function removeProductionPlace(index) {
  formDataApply.value.productPlaceFields.splice(index, 1);
};

console.log(props.formDataApplyObj); // 'test'
</script>

<style scoped>
.productionplace-container {
  margin-top: 5rem;
}

.my-field .v-icon {
  color: red !important;
}
</style>
