<template>
    <v-layout row>
      <v-flex xs6 offset-xs3>
        <div class="white elevation-2">
          <v-toolbar flat dark dense color="primary">
            <v-toolbar-title>Register</v-toolbar-title>
          </v-toolbar>
          <v-form class="pr-4 pl-4">
            <v-text-field
              v-model="email"
              label="Email"
              required
            ></v-text-field>
            <v-text-field
              v-model="password"
              label="Password"
              required
            ></v-text-field>
            <div class="errormsg" v-html="error" />
            <v-btn @click="register" class="primary">Register</v-btn>
          </v-form>
        </div>
      </v-flex>
    </v-layout>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
export default {
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  methods: {
    async register () {
      try {
        await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
      } catch (err) {
        this.error = err.response.data.error
      }
    }
  }
}
</script>

<style scoped>
.errormsg {
  color: red;
}
</style>
