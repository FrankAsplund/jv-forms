<template>
  <div class="d-flex bg-light-green-lighten-4 justify-center h-100">
    <v-container class="rounded mx-12">
      <v-card class="rounded-t-lg">
        <v-toolbar
          class="bg-light-blue-lighten-5 text-h5 font-weight-bold justify-center elevation-4"
          dark
        >
          <v-breadcrumbs :items="items">
            <template v-slot:title="{ item }">
              {{ item.title }}
            </template>
          </v-breadcrumbs>
          <v-toolbar-title class="text-h5 font-weight-bold"
            >{{ currentTitle }}
          </v-toolbar-title>
        </v-toolbar>

        <v-card-actions>
          <v-btn
            v-if="step > 1"
            size="x-large"
            icon="mdi-arrow-left-bold"
            color="black"
            @click="step--"
          ></v-btn>
          <v-spacer></v-spacer>
          <v-btn
            v-if="step < 4"
            size="x-large"
            icon="mdi-arrow-right-bold"
            color="black"
            @click="step++"
          ></v-btn>
        </v-card-actions>

        <v-window v-model="step" class="mx-12">
          <v-window-item :value="1">
            <Form />
          </v-window-item>

          <v-window-item :value="2">
            <FormApply />
          </v-window-item>

          <v-window-item :value="3">
            <FormSummary />
          </v-window-item>

          <v-window-item :value="4">
            <FormDone />
          </v-window-item>
        </v-window>
      </v-card>
    </v-container>
  </div>
</template>

<script>
export default {
  components: {
    Form,
    FormApply,
    FormSummary,
    FormDone,
  },
  name: "Home",
  data: () => ({
    step: 1,
    items: [
      {
        title: "Grunduppgifter",
        disabled: false,
      },
      {
        title: "Ansökan",
        disabled: true,
      },
      {
        title: "Summering",
        disabled: true,
      },
      {
        title: "Klar",
        disabled: true,
      },
    ],
  }),

  methods: {
    updateDisabled() {
      this.items.forEach((item, index) => {
        item.disabled = index !== this.step - 1;
      });
    },

    submitForm() {
      var config = {
        method: "POST",
        url: "https://dummy.restapiexample.com/api/v1/create",
        headers: {
          "Content-Type": "application/json",
        },
        data: JSON.stringify(this.formData),
      };

      axios(config)
        .then((response) => {
          this.response = JSON.stringify(response.data);
          console.log(JSON.stringify(response.data));
          document.forms[0].reset();
          this.success = true;
          this.error = false;
        })
        .catch((error) => {
          console.log(error);
          this.error = error.message;
          this.success = false;
        });
    },
  },
  computed: {
    currentTitle() {
      this.updateDisabled(); // Update disabled property based on current step
    },

    currentItem() {
      return this.items[this.step - 1];
    },
  },
};
</script>

<script setup>
import Form from "../components/Form.vue";
import FormApply from "../components/FormApply.vue";
import FormSummary from "../components/FormSummary.vue";
import FormDone from "../components/FormDone.vue";
</script>

<!-- <script lang="ts" setup>
import { useVModel } from '@vueuse/core'

const props = defineProps<{
  modelValue: string
}>()
const emit = defineEmits(['update:modelValue'])

const data = useVModel(props, 'modelValue', emit)
</script> -->

<style></style>
