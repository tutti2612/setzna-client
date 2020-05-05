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
        <v-row>
          <v-textarea rows="1" hide-details auto-grow outlined name="inputText" v-model="content"></v-textarea>
          <v-btn
            class="ml-2"
            height="55"
            depressed
            small
            color="primary"
            @click="submit"
            :disabled="content === ''"
          >
            <v-icon dark>mdi-pencil</v-icon>
          </v-btn>
        </v-row>
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
</style>