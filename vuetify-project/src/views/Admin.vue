<template>
  <div class="d-flex bg-indigo-lighten-4 justify-center h-100">
    <v-container class="rounded mx-12 mt-16" :elevation="12">
      <v-app>
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
                  {{ post.applicant_firstname }} {{ post.applicant_lastname }}
                </div>
                <!-- <div class="text-overline mb-1">Titel: {{ post.title }}</div> -->
                <div class="text-caption">
                  Telefonnummer: {{ post.applicant_customer_number }}
                </div>
                <div class="text-caption">E-post: {{ post.contact_email }}</div>
                <div class="text-caption">Avdelning: {{ post.department }}</div>
                <div class="text-caption">
                  Behörighet: {{ post.applicant_type }}
                </div>
                <div class="text-caption">
                  {{ post.applicant_county_name }}
                </div>
                <div class="text-caption">Län: {{ post.applicant_county }}</div>
              </div>
            </v-card-item>
            <v-card-actions>
              <v-btn variant="tonal" color="red" @click="deleteData(post.id)">
                Delete user
              </v-btn>

              <!-- Modal -->

              <v-dialog v-model="dialog" class="w-50 h-75">
                <template v-slot:activator="{ props }">
                  <v-btn variant="tonal" color="success" v-bind="props"
                    >Läs mer</v-btn
                  >
                </template>

                <v-card>
                  <v-card-text>
                    <v-table density="compact">
                      {{ post.application_poultry ? "Ja" : "Nej" }}
                      {{ post.application_area ? "Ja" : "Nej" }}
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
      </v-app>
    </v-container>
  </div>
</template>

<script setup>
import axios from "axios";
import { ref, onMounted } from "vue";

const dialog = ref(false);
const posts = ref([]);
const search = ref("");

const deleteData = async (id) => {
  if (
    confirm(
      "Are you sure you want to delete this user from the database? This choice is permanent and cannot be regretted."
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
    const data = response.data;
    if (search.value) {
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
      posts.value = data;
    }
  } catch (error) {
    console.log(error);
  }
};

onMounted(() => {
  console.log("Mounted");
  getAllPosts();
});
</script>
