<template>
  <v-app id="room">
    <v-content class="grey lighten-4 pt-0">
      <v-container class="cardContainer" fluid>
        <div v-for="message in messages" :key="message.name">
          <Card v-bind="message" />
        </div>
      </v-container>
    </v-content>
    <v-footer color="white" elevation="24" height="auto" fixed>
      <v-container class="textContainer" fluid>
        <v-textarea rows="1" counter="255" auto-grow outlined name="inputText" v-model="content"></v-textarea>
        <v-btn class="float-right" color="primary" @click="submit" :disabled="content === ''">Submit</v-btn>
      </v-container>
    </v-footer>
  </v-app>
</template>

<script lang="ts">
import Vue from "vue";
import Card from "@/components/Card.vue";

interface Message {
  name: string;
  content: string;
}

export default Vue.extend({
  name: "Room",
  components: {
    Card
  },
  props: {
    name: { type: String }
  },
  data: () => ({
    content: "",
    messages: [] as Message[]
  }),
  methods: {
    submit() {
      this.messages.push({ name: this.name, content: this.content });
      this.content = "";
    }
  }
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