<template>
  <v-app id="room">
    <v-content class="grey lighten-4 pt-0">
      <v-container class="cardContainer" fluid>
        <div v-for="message in messages" :key="message.createdAt">
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
            :disabled="content === '' && !isWsOpened"
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
  createdAt: string;
}

export default Vue.extend({
  name: "Room",
  components: {
    Card
  },
  props: {
    name: { type: String, default: "John Doe" }
  },
  data: () => ({
    content: "",
    messages: [] as Message[],
    latitude: 123.1234, //TODO: 端末の緯度を取得する
    longitude: 65.4567, //TODO: 端末の経度を取得する
    ws: {} as WebSocket,
    isWsOpened: false
  }),
  created: function() {
    this.ws = new WebSocket(
      `wss://g9nun1ag6h.execute-api.ap-northeast-1.amazonaws.com/Prod?latitude=${this.latitude}&longitude=${this.longitude}`
    );
    this.ws.onopen = () => {
      console.log("WebSocket has been opened.");
      this.isWsOpened = true;
    };
    this.ws.onmessage = msg => {
      console.log("Received a message.");
      console.log(msg);
      this.messages.push(JSON.parse(msg.data));
    };
    this.ws.onerror = e => {
      console.error("WebSocket error observed:", e);
    };
  },
  beforeDestroy: function() {
    this.ws.close();
    console.log("WebSocket has been closed.");
  },
  methods: {
    submit() {
      // this.messages.push({ name: this.name, content: this.content });
      const sendData = {
        message: "sendmessage",
        data: {
          name: this.name,
          content: this.content,
          createdAt: Date.now()
        }
      };
      this.ws.send(JSON.stringify(sendData));
      this.content = "";
      console.log("Sent a messege.");
    }
  }
});
</script>

<style lang="scss" scoped>
.cardContainer {
  padding-bottom: 700px;
}
</style>