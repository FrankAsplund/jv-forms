<template>
  <div class="mt-12">
    <v-bottom-navigation :elevation="8" grow class="bg-indigo-darken-1">
      <v-btn value="recent">
        <v-icon>mdi-twitter</v-icon>

        <a href="Twitter.com">Twitter</a>
      </v-btn>

      <v-btn value="favorites">
        <v-icon>mdi-github</v-icon>

        <a href="https://github.com/FrankAsplund/jv-forms">Github</a>
      </v-btn>

      <v-btn value="nearby">
        <v-icon>mdi-school</v-icon>

        <a href="https://kyh.se/">School</a>
      </v-btn>
    </v-bottom-navigation>
  </div>
</template>

<style scoped>
a {
  text-decoration: none !important;
  text-decoration-line: none !important;
}
</style>
