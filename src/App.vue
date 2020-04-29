<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <v-toolbar-title>Setzna</v-toolbar-title>
    </v-app-bar>

    <v-content>
      <Login />
    </v-content>
  </v-app>
</template>

<script lang="ts">
import Vue from "vue";
import Login from "./components/Login.vue";

export default Vue.extend({
  name: "App",

  components: {
    Login
  },

  data: () => ({
    //
  })
});
</script>
