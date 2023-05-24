<template>
  <v-form v-if="v$" validate-on="submit" variant="filled">
    <v-container class="pa-2 rounded-sm align-items">
      <custom-body>Undersökning för mental hälsa</custom-body>

      <v-hover v-slot="{ isHovering, props: hprops }">
        <v-card
          class="w-75 h-75 my-4"
          v-bind="hprops"
          :color="isHovering ? 'light-green-lighten-5' : undefined"
        >
          <v-checkbox
            v-model="v$.data.application_check.$model"
            label="Jag mår fysiskt och mentalt bra de flesta dagarna"
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
            v-model="v$.data.application_expand.$model"
            label="Jag är villig att besvara ytterligare frågor om min hälsa"
            color="success"
            hide-details
          ></v-checkbox>
        </v-card>
      </v-hover>
      <v-container v-if="v$.data.application_expand.$model">
        <v-checkbox
          v-model="v$.data.application_expand_mental.$model"
          label="Jag vill besvara frågor om min mentala hälsa"
          color="success"
          hide-details
        />
        <v-card
          v-if="v$.data.application_expand_mental.$model"
          class="w-100 h-75 my-4"
        >
          <v-slider
            v-model.number="
              v$.data.application_expand_mental_anxiety_slider.$model
            "
            :error-messages="
              v$.data.application_expand_mental_anxiety_slider.$errors[0]
                ?.$message
            "
            step="10"
            show-ticks="always"
            label="Hur mycket ångest eller oro upplever du ungefär per månad?"
            tick-size="4"
          ></v-slider>

          <v-slider
            v-model.number="
              v$.data.application_expand_mental_stress_slider.$model
            "
            :error-messages="
              v$.data.application_expand_mental_anxiety_slider.$errors[0]
                ?.$message
            "
            step="10"
            show-ticks="always"
            label="Hur bra är du på att hantera stress i din vardag?"
            tick-size="4"
          ></v-slider>

          <v-slider
            v-model.number="
              v$.data.application_expand_mental_health_slider.$model
            "
            :error-messages="
              v$.data.application_expand_mental_health_slider.$errors[0]
                ?.$message
            "
            step="10"
            show-ticks="always"
            label="Hur bra skulle du säga att din mentala hälsa är, allmänt?"
            tick-size="4"
          ></v-slider>
        </v-card>
      </v-container>

      <v-container v-if="v$.data.application_expand.$model">
        <v-checkbox
          v-model="v$.data.application_expand_physical.$model"
          label="Jag vill besvara frågor om min fysiska hälsa"
          color="success"
          hide-details
        />
        <v-card
          v-if="v$.data.application_expand_physical.$model"
          class="w-100 h-75 ma-2"
        >
          <v-slider
            v-model.number="
              v$.data.application_expand_physical_health_slider.$model
            "
            :error-messages="
              v$.data.application_expand_physical_health_slider.$errors[0]
                ?.$message
            "
            step="10"
            show-ticks="always"
            label="Hur skulle du bedöma din allmänna fysiska hälsa?"
            tick-size="4"
          ></v-slider>

          <v-slider
            v-model.number="
              v$.data.application_expand_physical_activity_slider.$model
            "
            :error-messages="
              v$.data.application_expand_physical_activity_slider.$errors[0]
                ?.$message
            "
            step="10"
            show-ticks="always"
            label="Hur ofta deltar du i regelbunden fysisk aktivitet, så som träning eller motion?"
            tick-size="4"
          ></v-slider>

          <v-slider
            v-model.number="
              v$.data.application_expand_physical_body_slider.$model
            "
            :error-messages="
              v$.data.application_expand_physical_body_slider.$errors[0]
                ?.$message
            "
            step="10"
            show-ticks="always"
            label="Hur nöjd är du med din kropp i överlag?"
            tick-size="4"
          ></v-slider>
          <!-- <v-text-field
            v-model.number="v$.data.application_expand_physical_older.$model"
            label="Ange genomsnittligt antal kalkoner över 24 veckor i din besättning 2023"
            prepend-icon="mdi:mdi-plus-box"
          ></v-text-field>

          <v-text-field
            v-model.number="v$.data.application_expand_physical_broilers.$model"
            label="Ange antal slaktkalkoner i en normal uppfödningsomgång under år 2023"
            prepend-icon="mdi:mdi-plus-box"
          ></v-text-field>

          <v-text-field
            v-model.number="v$.data.application_expand_physical_egg.$model"
            label="Ange genomsnittligt antal kalkonkycklingar för äggproduktion i din besättning 2023"
            prepend-icon="mdi:mdi-plus-box"
          ></v-text-field>

          <v-text-field
            v-model="application_expand_physical_total_count"
            label="Total summa"
            readonly
            prepend-icon="mdi:mdi-equal-box"
          ></v-text-field>
 -->
          <!-- <custom-body class="mx-2">Anläggning</custom-body>
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
          </v-container> -->
        </v-card>
      </v-container>
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
      application_check: false,
      application_expand: false,

      application_expand_mental_anxiety_slider: null,
      application_expand_mental_stress_slider: null,
      application_expand_mental_health_slider: null,

      application_expand_mental: false,
      application_expand_physical: false,

      application_expand_physical_health_slider: null,
      application_expand_physical_activity_slider: null,
      application_expand_physical_body_slider: null,

      // Initial value in Product Place fields array
      /* application_sites_turkeys: [{ value: "" }],
      application_sites_hens: [{ value: "" }], */
    }),
  },
  valid: {
    type: Boolean,
    default: false,
  },
});

/* const application_expand_mental_total_count = computed(
  () =>
    Number(props.formDataApplyObj.application_expand_mental_older) +
    Number(props.formDataApplyObj.application_expand_mental_broilers) +
    Number(props.formDataApplyObj.application_expand_mental_egg)
);

const application_expand_physical_total_count = computed(
  () =>
    Number(props.formDataApplyObj.application_expand_physical_older) +
    Number(props.formDataApplyObj.application_expand_physical_broilers) +
    Number(props.formDataApplyObj.application_expand_physical_egg)
); */

const emit = defineEmits([
  "update:modelValue",
  "update:formDataApplyObj",
  "update:valid",
]);
const { formDataApplyObj: formDataApply, valid: isFormValid } = useVModels(
  props,
  emit
);

/* function addProductionPlaceHens() {
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
} */

/* const files = ref([]); */

const rules = computed(() => ({
  data: {
    application_check: {
      // Custom validator here because checkboxes return `true` or `false` and both satisfies the `required` validator provided by vuelidate
      requiredUnless: (value) =>
        value === true || !!formDataApply.value.application_expand,
    },

    application_expand: {},

    application_expand_mental: {
      requiredUnless: (value) =>
        // Custom validator here because we only check validation if `application_expand` is checked and if `application_expand_physical` is not checked
        value === true ||
        !formDataApply.value.application_expand ||
        !!formDataApply.value.application_expand_physical,
    },

    application_expand_physical: {
      requiredUnless: (value) =>
        // Custom validator here because we only check validation if `application_expand` is checked and if `application_expand_physical` is not checked
        value === true ||
        !formDataApply.value.application_expand ||
        !!formDataApply.value.application_expand_mental,
    },

    application_expand_mental_anxiety_slider: {
      /* numeric, */
    },
    application_expand_mental_stress_slider: {
      /* numeric, */
    },
    application_expand_mental_health_slider: {
      /* numeric, */
    },

    application_expand_physical_health_slider: {
      /* numeric, */
    },
    application_expand_physical_activity_slider: {
      /* numeric, */
    },
    application_expand_physical_body_slider: {
      /* numeric, */
    },
  },

  application_expand_mental_total_count: {},

  application_expand_physical_total_count: {},
}));

const v$ = useVuelidate(rules, {
  data: formDataApply.value,
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
