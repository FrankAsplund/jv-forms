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

      <v-container v-if="formDataApply.productionType">
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

            <v-text-field label="Total summa" v-model="totalHens" readonly prepend-icon="mdi-equal-box"></v-text-field>
          </v-card>
        </v-container>
      </v-container>

      <v-container v-if="formDataApply.productionType">
        <v-container>
          <v-checkbox label="Kalkonproduktion" color="success" v-model="showTurkeys" hide-details />
          <v-card class="w-100 h-75 my-4" v-if="showTurkeys">
            <v-text-field v-model="field4" label="Ange genomsnittligt antal kalkoner över 24 veckor i din besättning 2023"
              prepend-icon="mdi-plus-box"></v-text-field>

            <v-text-field v-model="field5" label="Ange antal slaktkalkoner i en normal uppfödningsomgång under år 2023"
              prepend-icon="mdi-plus-box"></v-text-field>

            <v-text-field v-model="average"
              label="Ange genomsnittligt antal kalkonkycklingar för äggproduktion i din besättning 2023"
              prepend-icon="mdi-plus-box"></v-text-field>

            <v-text-field label="Total summa" v-model="totalTurkeys" readonly prepend-icon="mdi-equal-box">
            </v-text-field>
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
import { useVModel } from "@vueuse/core";
import { defineProps } from "vue";
import { computed } from 'vue'

const props = defineProps({
  formDataApplyObj: {
    type: Object,
    default: () => ({
      productionType: false,
      showHens: false,
      showTurkeys: false,
      totalHens: 0,
      totalTurkeys: 0,
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


const totalHens = computed(
  () =>
    Number(props.formDataApplyObj.field1) +
    Number(props.formDataApplyObj.field2) +
    Number(props.formDataApplyObj.field3)
);

const totalTurkeys = computed(
  () =>
    Number(props.formDataApplyObj.field4) +
    Number(props.formDataApplyObj.field5) +
    Number(props.formDataApplyObj.field6)
);
</script>

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
      showTurkeys: false,
      field1: 0,
      field2: 0,
      field3: 0,
      field4: 0,
      field5: 0,
      field6: 0,
      totalHens: 0,
      totalTurkeys: 0,
      productPlaceFields: [],
    };
  }
};
</script>

<style scoped>
.productionplace-container {
  margin-top: 5rem;
}

.my-field .v-icon {
  color: red !important;
}
</style>
