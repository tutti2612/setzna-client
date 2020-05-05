<template>
  <v-card class="mx-auto" color="white" max-width="400">
    <v-card-text class="headline">{{content}}</v-card-text>

    <v-card-actions>
      <v-list-item class="grow">
        <v-list-item-avatar color="grey darken-3">
          <v-img
            class="elevation-6"
            src="https://avatars1.githubusercontent.com/u/19503423?s=460&u=9a0de00b7f6ac5051208f67e022cfe300ba0a159&v=4"
          ></v-img>
        </v-list-item-avatar>

        <v-list-item-content>
          <v-list-item-title>{{name}}</v-list-item-title>
        </v-list-item-content>

        <!-- <v-row align="center" justify="end">
          <v-icon class="mr-1">mdi-heart</v-icon>
          <span class="subheading mr-2">256</span>
          <v-icon class="mr-1">mdi-share-variant</v-icon>
          <span class="subheading">45</span>
        </v-row>-->
      </v-list-item>
    </v-card-actions>
  </v-card>
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  name: "Card",
  props: {
    name: { type: String, default: "John Doe" },
    content: { type: String, default: "" }
  }
});
</script>

<style lang="scss" scoped>
.v-card {
  margin-bottom: 12px;
}
</style>>