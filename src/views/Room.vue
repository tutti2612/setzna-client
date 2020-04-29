<template>
  <v-app id="room">
    <v-content class="grey lighten-4 pt-0">
      <v-container class="cardContainer" fluid>
        <Card />
        <Card />
        <Card />
      </v-container>
    </v-content>
    <v-footer color="white" elevation="24" height="auto" fixed>
      <v-container class="textContainer" fluid>
        <v-textarea rows="1" counter="255" auto-grow outlined name="inputText" v-model="text"></v-textarea>
        <v-btn class="float-right" color="primary">Submit</v-btn>
      </v-container>
    </v-footer>
  </v-app>
</template>

<script lang="ts">
import Vue from "vue";
import Card from "@/components/Card.vue";
export default Vue.extend({
  name: "Room",
  components: {
    Card
  },
  data: () => ({
    text: ""
  })
});
</script>

<style lang="scss" scoped>
.cardContainer {
  padding-bottom: 700px;
}
.textContainer {
  padding-left: 0;
  padding-right: 0;
}
</style>