<template>
  <v-app id="inspire">
    <v-content>
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="4">
            <v-card class="elevation-12">
              <v-toolbar color="primary" dark flat>
                <v-toolbar-title>Login form</v-toolbar-title>
              </v-toolbar>
              <v-card-text>
                <v-form ref="form" v-model="valid">
                  <v-text-field v-model="name" label="Name" name="name" type="text" :counter="10" :rules="nameRules" required />

                  <!-- <v-text-field
                    id="password"
                    label="Password"
                    name="password"
                    prepend-icon="lock"
                    type="password"
                  />-->
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer />
                <v-btn color="primary" @click="validate">Login</v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "Login",

  data: () => ({
    valid: true,
    name: '',
    nameRules: [
        (v: string) => !!v || 'Name is required',
        (v: string) => (v && v.length <= 10) || 'Name must be less than 10 characters',
      ],
  }),
  methods: {
    validate() {
      (this.$refs.form as Vue & { validate: () => boolean }).validate()
    }
  }
});
</script>