<template>
  <v-form v-if="v$" validate-on="submit" variant="filled">
    <v-container class="pa-2 rounded-sm align-items">
      <custom-body>Produktion</custom-body>

      <v-hover v-slot="{ isHovering, props: hprops }">
        <v-card
          class="w-75 h-75 my-4"
          v-bind="hprops"
          :color="isHovering ? 'light-green-lighten-5' : undefined"
        >
          <v-checkbox
            v-model="v$.data.application_area.$model"
            label="Jag söker krisstöd för areal"
            color="success"
            hide-details
          ></v-checkbox>
        </v-card>
      </v-hover>

      <v-hover v-slot="{ isHovering, props: hprops }">
        <v-card
          class="w-75 h-75 my-4"
          v-bind="hprops"
          :color="isHovering ? 'light-green-lighten-5' : undefined"
        >
          <v-checkbox
            v-model="v$.data.application_poultry.$model"
            label="Jag söker krisstöd för min fjäderfäproduktion"
            color="success"
            hide-details
          ></v-checkbox>
        </v-card>
      </v-hover>
      <v-container v-if="v$.data.application_poultry.$model">
        <v-checkbox
          v-model="v$.data.application_poultry_hens.$model"
          label="Hönsproduktion"
          color="success"
          hide-details
        />
        <v-card
          v-if="v$.data.application_poultry_hens.$model"
          class="w-100 h-75 my-4"
        >
          <v-text-field
            v-model.number="v$.data.application_poultry_hens_older.$model"
            :error-messages="
              v$.data.application_poultry_hens_older.$errors[0]?.$message
            "
            type="number"
            label="Ange genomsnittlig antal höns äldre än 20 veckor i din besättning 2023"
            prepend-icon="mdi:mdi-plus-box"
          ></v-text-field>

          <v-text-field
            v-model.number="v$.data.application_poultry_hens_broilers.$model"
            :error-messages="
              v$.data.application_poultry_hens_broilers.$errors[0]?.$message
            "
            type="number"
            label="Ange antal slaktkycklingar i en normal uppfödningsomgång under år 2023"
            prepend-icon="mdi:mdi-plus-box"
          ></v-text-field>

          <v-text-field
            v-model.number="v$.data.application_poultry_hens_egg.$model"
            type="number"
            label="Ange genomsnittligt antal kycklingar för äggproduktion i din besättning 2023"
            prepend-icon="mdi:mdi-plus-box"
          ></v-text-field>

          <v-text-field
            v-model="application_poultry_hens_total_count"
            :error-messages="
              v$.application_poultry_hens_total_count.$errors[0]?.$message
            "
            label="Total summa"
            readonly
            prepend-icon="mdi:mdi-equal-box"
          ></v-text-field>

          <custom-body class="mx-2">Anläggning</custom-body>
          <v-container class="ma-2">
            <div class="text-subtitle-1">
              Om du har dina höns i en kommersiell verksamhet måste du ange
              produktionsplats.
            </div>
            <v-text-field
              v-if="formDataApply.application_sites_hens?.[0]"
              v-model="formDataApply.application_sites_hens[0].value"
              label="Produktionsplatsnummer"
              prefix="SE"
              hint="Ange den/de produktionsplatser där du bedrev din produktion 2023. Varje nummer består av upp till 6 siffor."
            ></v-text-field>
            <v-text-field
              v-for="(
                field, index
              ) in formDataApply.application_sites_hens.slice(1)"
              :key="index"
              v-model="field.value"
              :label="'Produktionsplatsnummer'"
              prefix="SE"
            >
              <template #append>
                <v-icon
                  :style="{ color: 'red' }"
                  @click="removeProductionPlaceHens(index)"
                  >mdi:mdi-delete</v-icon
                >
              </template>
            </v-text-field>
            <v-btn
              prepend-icon="mdi:mdi-plus"
              color="success"
              class="my-4"
              @click="addProductionPlaceHens"
            >
              Lägg till produktionsplats
            </v-btn>
          </v-container>
        </v-card>
      </v-container>

      <v-container v-if="v$.data.application_poultry.$model">
        <v-checkbox
          v-model="v$.data.application_poultry_turkeys.$model"
          label="Kalkonproduktion"
          color="success"
          hide-details
        />
        <v-card
          v-if="v$.data.application_poultry_turkeys.$model"
          class="w-100 h-75 ma-2"
        >
          <v-text-field
            v-model.number="v$.data.application_poultry_turkeys_older.$model"
            label="Ange genomsnittligt antal kalkoner över 24 veckor i din besättning 2023"
            prepend-icon="mdi:mdi-plus-box"
          ></v-text-field>

          <v-text-field
            v-model.number="v$.data.application_poultry_turkeys_broilers.$model"
            label="Ange antal slaktkalkoner i en normal uppfödningsomgång under år 2023"
            prepend-icon="mdi:mdi-plus-box"
          ></v-text-field>

          <v-text-field
            v-model.number="v$.data.application_poultry_turkeys_egg.$model"
            label="Ange genomsnittligt antal kalkonkycklingar för äggproduktion i din besättning 2023"
            prepend-icon="mdi:mdi-plus-box"
          ></v-text-field>

          <v-text-field
            v-model="application_poultry_turkeys_total_count"
            label="Total summa"
            readonly
            prepend-icon="mdi:mdi-equal-box"
          ></v-text-field>

          <custom-body class="mx-2">Anläggning</custom-body>
          <v-container class="ma-2">
            <div class="text-subtitle-1">
              Om du har dina kalkoner i en kommersiell verksamhet måste du ange
              produktionsplats.
            </div>
            <v-text-field
              v-if="formDataApply.application_sites_turkeys?.[0]"
              v-model="formDataApply.application_sites_turkeys[0].value"
              label="Produktionsplatsnummer"
              prefix="SE"
              hint="Ange den/de produktionsplatser där du bedrev din produktion 2023. Varje nummer består av upp till 6 siffor."
            ></v-text-field>
            <v-text-field
              v-for="(
                field, index
              ) in formDataApply.application_sites_turkeys.slice(1)"
              :key="index"
              v-model="field.value"
              :label="'Produktionsplatsnummer'"
              prefix="SE"
            >
              <template #append>
                <v-icon
                  :style="{ color: 'red' }"
                  @click="removeProductionPlaceTurkeys(index)"
                  >mdi:mdi-delete</v-icon
                >
              </template>
            </v-text-field>
            <v-btn
              prepend-icon="mdi:mdi-plus"
              color="success"
              class="my-4"
              @click="addProductionPlaceTurkeys"
            >
              Lägg till produktionsplats
            </v-btn>
          </v-container>
        </v-card>
      </v-container>
      <!--       <v-file-input
        v-model="selectedFiles"
        multiple
        label="Bifoga filer"
        accept="image/png, image/jpeg, .png, .jpg, .jpeg .doc, .docx, .xml,application/msword, application/vnd.openxmlformats-officedocument.wordprocessingml.document"
        class="w-75 h-75"
        show-size
        persistent-hint
        hint="Bifoga filer du vill skicka med här. Valda filer får ej överskrida 5MB"
      ></v-file-input> -->
    </v-container>
  </v-form>
</template>

<script setup>
import CustomBody from "../form-components/c-body.vue";
import { useVModels } from "@vueuse/core";
import { ref, computed, watchEffect, watch } from "vue";
import { useVuelidate } from "@vuelidate/core";
import { required, numeric, minValue, helpers } from "@vuelidate/validators";

const props = defineProps({
  formDataApplyObj: {
    type: Object,
    default: () => ({
      application_area: false,
      application_poultry: false,

      application_poultry_hens_older: null,
      application_poultry_hens_broilers: null,
      application_poultry_hens_egg: null,

      application_poultry_hens: false,
      application_poultry_turkeys: false,

      application_poultry_turkeys_older: null,
      application_poultry_turkeys_broilers: null,
      application_poultry_turkeys_egg: null,

      // Initial value in Product Place fields array
      application_sites_turkeys: [{ value: "" }],
      application_sites_hens: [{ value: "" }],
    }),
  },
  valid: {
    type: Boolean,
    default: false,
  },
  /*   selectedFiles: {
    type: Array,
    default: [],
  }, */
});

const application_poultry_hens_total_count = computed(
  () =>
    Number(props.formDataApplyObj.application_poultry_hens_older) +
    Number(props.formDataApplyObj.application_poultry_hens_broilers) +
    Number(props.formDataApplyObj.application_poultry_hens_egg)
);

const application_poultry_turkeys_total_count = computed(
  () =>
    Number(props.formDataApplyObj.application_poultry_turkeys_older) +
    Number(props.formDataApplyObj.application_poultry_turkeys_broilers) +
    Number(props.formDataApplyObj.application_poultry_turkeys_egg)
);

const emit = defineEmits([
  "update:modelValue",
  "update:formDataApplyObj",
  "update:valid",
]);
const { formDataApplyObj: formDataApply, valid: isFormValid } = useVModels(
  props,
  emit
);

function addProductionPlaceHens() {
  formDataApply.value.application_sites_hens.push({ value: "" });
}

function removeProductionPlaceHens(index) {
  formDataApply.value.application_sites_hens.splice(index, 1);
}

function addProductionPlaceTurkeys() {
  formDataApply.value.application_sites_turkeys.push({ value: "" });
}

function removeProductionPlaceTurkeys(index) {
  formDataApply.value.application_sites_turkeys.splice(index, 1);
}

const files = ref([]);

/* watch(
  () => props.selectedFiles,
  (newVal) => {
    files.value = newVal;

    files.value.forEach((file) => {
      if (file.size > 1024 * 1024 * 5) {
        selectedFiles.value = [];
        alert("Den valda filen är för stor, vänligen välj en fil under 5MB");
      }
    });
  }
); */

const rules = computed(() => ({
  data: {
    application_area: {
      // Custom validator here because checkboxes return `true` or `false` and both satisfies the `required` validator provided by vuelidate
      requiredUnless: (value) =>
        value === true || !!formDataApply.value.application_poultry,
    },

    application_poultry: {},

    application_poultry_hens: {
      requiredUnless: (value) =>
        // Custom validator here because we only check validation if `application_poultry` is checked and if `application_poultry_turkeys` is not checked
        value === true ||
        !formDataApply.value.application_poultry ||
        !!formDataApply.value.application_poultry_turkeys,
    },

    application_poultry_turkeys: {
      requiredUnless: (value) =>
        // Custom validator here because we only check validation if `application_poultry` is checked and if `application_poultry_turkeys` is not checked
        value === true ||
        !formDataApply.value.application_poultry ||
        !!formDataApply.value.application_poultry_hens,
    },

    application_poultry_hens_older: {
      numeric,
    },
    application_poultry_hens_broilers: {
      numeric,
    },
    application_poultry_hens_egg: {
      numeric,
    },

    application_poultry_turkeys_older: {
      numeric,
    },
    application_poultry_turkeys_broilers: {
      numeric,
    },
    application_poultry_turkeys_egg: {
      numeric,
    },
    application_sites_turkeys: {
      // We need this to specify that `application_site_hens` is an array and we need to implement validation for each element/child
      $each: helpers.forEach({
        value: {
          // Custom validator here because we only need to check validation if `application_poultry_hens` is true/checked
          isRequired: (value) =>
            !formDataApply.value.application_poultry_turkeys ||
            required.$validator(value),
        },
      }),
    },
    application_sites_hens: {
      // We need this to specify that `application_site_hens` is an array and we need to implement validation for each element/child
      $each: helpers.forEach({
        value: {
          // Custom validator here because we only need to check validation if `application_poultry_hens` is true/checked
          isRequired: (value) =>
            !formDataApply.value.application_poultry_hens ||
            required.$validator(value),
        },
      }),
    },
  },

  application_poultry_hens_total_count: {
    // Custom validator here because we only need to check validation if `application_poultry_hens` is true/checked
    moreThanOne: (value) =>
      !formDataApply.value.application_poultry_hens ||
      minValue(1).$validator(value),
  },

  application_poultry_turkeys_total_count: {
    // Custom validator here because we only need to check validation if `application_poultry_hens` is true/checked
    moreThanOne: (value) =>
      !formDataApply.value.application_poultry_turkeys ||
      minValue(1).$validator(value),
  },
}));

const v$ = useVuelidate(rules, {
  data: formDataApply.value,
  application_poultry_hens_total_count,
});

watchEffect(() => {
  isFormValid.value = !v$.value.$invalid;
});
</script>

<style scoped>
.v-container {
  padding: 2px !important;
}

.my-field .v-icon {
  color: red !important;
}
</style>
