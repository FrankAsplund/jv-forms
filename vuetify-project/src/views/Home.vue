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
            <Form @submit.prevent="submitForm" />
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

<script setup>
import Form from "../components/Form.vue";
import FormApply from "../components/FormApply.vue";
import FormSummary from "../components/FormSummary.vue";
import FormDone from "../components/FormDone.vue";

import axios from "axios";

async function submitForm() {
  const formData = {
    firstname: "John",
    lastname: "Doe",
    ssn: "12456-1234",
    email: this.email,
    apply: this.apply,
    applyCounty: this.applyCounty,
    applyNumber: this.applyNumber,
  };

  try {
    const response = await axios.post(
      "https://dummy.restapiexample.com/api/v1/create",
      formData,
      {
        headers: {
          "Content-Type": "application/json",
        },
      }
    );

    /* this.response = response.data; */
    console.log(response.data);
    document.forms[0].reset();
  } catch (error) {
    console.log(error);
  }
}
</script>

<script>
export default {
  components: {
    Form,
    FormApply,
    FormSummary,
    FormDone,
  },
  name: "Home",
  data() {
    return {
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

      formData: {
        firstname: "John",
        lastname: "Doe",
        ssn: "12456-1234",
        email: "",
        apply: "",
        applyCounty: "",
        applyNumber: "",
      },
    };
  },

  methods: {
    updateDisabled() {
      this.items.forEach((item, index) => {
        item.disabled = index !== this.step - 1;
      });
    },
  },

  /* async submitForm() {
      const formData = {
        name: this.name,
        email: this.email,
        apply: this.apply,
        applyCounty: this.applyCounty,
        applyNumber: this.applyNumber,
      };

      const response = await fetch('https://dummy.restapiexample.com/api/v1/create', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(formData)
      });

      if (response.ok) {

      } else {

      }
    }, */

  /* submitForm() {
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
        })
        .catch((error) => {
          console.log(error);
        });
    },
  }, */
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

<style></style>
