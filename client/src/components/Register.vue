<template>
    <v-layout row>
      <v-flex xs6 offset-xs3>
        <panel title="Register">
          <v-form class="pr-4 pl-4" autocomplete="off">
            <v-text-field
              v-model="email"
              label="Email"
              required
            ></v-text-field>
            <v-text-field
              v-model="password"
              label="Password"
              type="Password"
              autocomplete="new-password"
              required
            ></v-text-field>
            <div class="errormsg" v-html="error" />
            <v-btn @click="register" class="primary">Register</v-btn>
          </v-form>
        </panel>
      </v-flex>
    </v-layout>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
import Panel from '@/components/Panel'

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
        const response = await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
        this.$store.dispatch('setToken', response.data.token)
        this.$store.dispatch('setUser', response.data.user)
      } catch (err) {
        this.error = err.response.data.error
      }
    }
  },
  components: {
    Panel
  }
}
</script>

<style scoped>
.errormsg {
  color: red;
}
</style>
