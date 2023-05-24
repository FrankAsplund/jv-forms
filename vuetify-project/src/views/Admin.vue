<template>
  <!-- <v-app> -->
  <div class="d-flex bg-indigo-lighten-4 justify-center h-100">
    <v-container class="rounded mx-12 mt-16" :elevation="12">
      <custom-header header="Alla inskickade formulär" />
      <v-card class="rounded-t-lg">
        <div class="d-flex justify-center ma-4">
          <v-text-field
            class="w-50 mx-12"
            prepend-icon="mdi-magnify"
            variant="outlined"
            type="text"
            v-model.trim="search"
            placeholder="Search for users..."
            @keyup="getAllPosts"
          >
          </v-text-field>
        </div>

        <div class="d-flex align-content-space-between flex-wrap ma-4 pa-2">
          <v-card
            v-for="post in posts"
            :key="post.id"
            class="ma-2 pa-2"
            min-width="300"
            max-width="300"
            variant="outlined"
            :elevation="12"
          >
            <v-card-subtitle> {{ post.id }} </v-card-subtitle>
            <v-card-item>
              <div>
                <div class="text-h6 mb-1">
                  {{ post.FormData.applicant_firstname }}
                  {{ post.FormData.applicant_lastname }}
                </div>
                <div class="text-caption">
                  Telefonnummer: {{ post.FormData.applicant_customer_number }}
                </div>
                <div class="text-caption">
                  E-post: {{ post.FormData.contact_email }}
                </div>
                <div class="text-caption">
                  Personnummer: {{ post.FormData.applicant_personal_number }}
                </div>
                <div class="text-caption">
                  Söktyp: {{ post.FormData.applicant_type }}
                </div>
                <!-- <div class="text-caption">
                  Län {{ post.FormData.applicant_county_name }}
                  {{ post.FormData.applicant_county }}
                </div> -->
              </div>
            </v-card-item>
            <v-card-actions>
              <v-btn
                class="text-none"
                prepend-icon="mdi-trash-can"
                variant="tonal"
                color="red"
                @click="deleteData(post.id)"
              >
                Radera inlägg
              </v-btn>

              <!-- Modal -->

              <v-dialog v-model="post.dialog" class="w-50 h-75">
                <template v-slot:activator="{ props }">
                  <v-btn
                    class="text-none"
                    prepend-icon="mdi-arrow-expand"
                    variant="tonal"
                    color="primary"
                    v-bind="props"
                    @click="selectedPost = post"
                  >
                    Läs mer
                  </v-btn>
                </template>

                <v-card>
                  <custom-header header="Detaljerad information" />
                  <v-card-text>
                    <v-table density="compact">
                      <thead>
                        <tr>
                          <th class="text-left">
                            "Jag mår fysiskt och mentalt bra de flesta dagarna"
                          </th>

                          <th class="text-right">
                            {{
                              post.FormApply.application_check ? "Ja" : "Nej"
                            }}
                          </th>
                        </tr>

                        <tr>
                          <th class="text-left">
                            "Jag är villig att besvara ytterligare frågor om min
                            hälsa"
                          </th>

                          <th class="text-right">
                            {{
                              post.FormApply.application_expand ? "Ja" : "Nej"
                            }}
                          </th>
                        </tr>

                        <tr>
                          <th class="text-left">
                            "Jag vill besvara frågor om min mentala hälsa"
                          </th>

                          <th class="text-right">
                            {{
                              post.FormApply.application_expand_mental
                                ? "Ja"
                                : "Nej"
                            }}
                          </th>
                        </tr>

                        <tr>
                          <th class="text-left">
                            "Hur mycket ångest eller oro upplever du ungefär per
                            månad?"
                          </th>

                          <th class="text-right">
                            {{
                              post.FormApply
                                .application_expand_mental_anxiety_slider
                            }}
                          </th>
                        </tr>

                        <tr>
                          <th class="text-left">
                            "Hur bra är du på att hantera stress i din vardag?"
                          </th>

                          <th class="text-right">
                            {{
                              post.FormApply
                                .application_expand_mental_stress_slider
                            }}
                          </th>
                        </tr>

                        <tr>
                          <th class="text-left">
                            "Hur bra skulle du säga att din mentala hälsa är,
                            allmänt?"
                          </th>

                          <th class="text-right">
                            {{
                              post.FormApply
                                .application_expand_mental_health_slider
                            }}
                          </th>
                        </tr>

                        <tr>
                          <th class="text-left">
                            "Jag vill besvara frågor om min fysiska hälsa"
                          </th>

                          <th class="text-right">
                            {{
                              post.FormApply.application_expand_physical
                                ? "Ja"
                                : "Nej"
                            }}
                          </th>
                        </tr>

                        <tr>
                          <th class="text-left">
                            "Hur skulle du bedöma din allmänna fysiska hälsa?"
                          </th>

                          <th class="text-right">
                            {{
                              post.FormApply
                                .application_expand_physical_health_slider
                            }}
                          </th>
                        </tr>

                        <tr>
                          <th class="text-left">
                            "Hur ofta deltar du i regelbunden fysisk aktivitet,
                            så som träning eller motion?"
                          </th>

                          <th class="text-right">
                            {{
                              post.FormApply
                                .application_expand_physical_activity_slider
                            }}
                          </th>
                        </tr>

                        <tr>
                          <th class="text-left">
                            "Hur nöjd är du med din kropp i överlag?"
                          </th>

                          <th class="text-right">
                            {{
                              post.FormApply
                                .application_expand_physical_body_slider
                            }}
                          </th>
                        </tr>
                      </thead>
                    </v-table>
                  </v-card-text>
                  <v-card-actions>
                    <v-btn color="error" @click="dialog = false">Stäng</v-btn>
                  </v-card-actions>
                </v-card>
              </v-dialog>
            </v-card-actions>
          </v-card>
        </div>
      </v-card>
    </v-container>
  </div>
  <!-- </v-app> -->
</template>

<script setup>
import axios from "axios";
import { ref, onMounted } from "vue";
import CustomHeader from "../components/form-components/c-header.vue";

const selectedPost = ref(null);

const posts = ref([
  {
    id: "",
    FormData: {},
    FormApply: {},

    dialog: false,
  },
]);

const search = ref(null);

const deleteData = async (id) => {
  if (
    confirm(
      "Är du säker på att du vill radera detta formuläret från databasen? Detta valet är permanent och kan inte ångras."
    )
  ) {
    try {
      const response = await axios.delete(`http://localhost:8000/posts/${id}`);
      if (response.status !== 200) {
        throw new Error(`Error ${response.status}`);
      }
      // Object was successfully deleted, do something with the response data
    } catch (error) {
      // There was an error deleting the object
      console.log(error);
    }

    console.log("Delete successful", `Post number ID: ${id} is now deleted`);
    getAllPosts();
  } else {
    return;
  }
};

const getAllPosts = async () => {
  try {
    const response = await axios.get("http://localhost:8000/posts");
    /* const data = response.data; */

    posts.value = response.data;
    /* console.log(data); */
    console.log(posts.value);
    /* if (search.value) {
      posts.value = data.filter(
        (post) =>
          post.applicant_firstname
            .toLowerCase()
            .includes(search.value.toLowerCase()) ||
          post.applicant_lastname
            .toLowerCase()
            .includes(search.value.toLowerCase()) ||
          post.applicant_personal_number
            .toLowerCase()
            .includes(search.value.toLowerCase()) ||
          post.contact_email
            .toLowerCase()
            .includes(search.value.toLowerCase()) ||
          post.applicant_customer_number
            .toLowerCase()
            .includes(search.value.toLowerCase()) ||
          post.applicant_type.toLowerCase().includes(search.value.toLowerCase())
      );
    } else {
      console.log(data);
      posts.value = response.data;
    } */
  } catch (error) {
    console.log(error);
  }
};

onMounted(() => {
  console.log("Mounted");
  getAllPosts();
});
</script>
