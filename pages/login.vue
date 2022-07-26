<template>
  <v-row class="d-flex justify-center align-center h-100 bg-blue pa-5">
    <v-col md="6" class="white pa-10 rounded-lg">

      <h1 class="text-center color-blue ma-0">Login</h1>
      <p class="text-center py-3">Welcome to the Insurance Commision Claims App.</p>

      <v-text-field v-model="email" color="purple darken-2" label="Email" required>
      </v-text-field>
      <v-text-field v-model="password" :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
        :rules="[rules.required, rules.min]" :type="show1 ? 'text' : 'password'" name="input-10-1" label="Password"
        hint="At least 8 characters" counter @click:append="show1 = !show1">
      </v-text-field>
      <p>Did you <a href="" class="color-blue text-decoration-none">forget your password?</a></p>

      <div v-if="this.$route.query.user === 'agency'">
        <nuxt-link to="/register">
          <v-btn rounded color="primary" block class="mt-5">
            Login
          </v-btn>
        </nuxt-link>
      </div>
      <div v-else-if="this.$route.query.user === 'insurance'">
        <nuxt-link to="/insurance/commision-claims">
          <v-btn rounded color="primary" block class="mt-5">
            Login
          </v-btn>
        </nuxt-link>
      </div>
      <div v-else-if="this.$route.query.user === 'payer'">
        <nuxt-link to="/cca/claims">
          <v-btn rounded color="primary" block class="mt-5">
            Login
          </v-btn>
        </nuxt-link>
      </div>
      <div v-else-if="this.$route.query.user === 'agents-dash'">
        <nuxt-link to="/agencies/commision-claim">
          <v-btn rounded color="primary" block class="mt-5">
            Login
          </v-btn>
        </nuxt-link>
      </div>

      <!-- <v-card>
        <h1 class="text-center color-blue">Login</h1>
        <p class="text-center py-3">Welcome to the Insurance Commision Claims App.</p>


        <v-text-field v-model="email" color="purple darken-2" label="Email" required>
        </v-text-field>
        <v-text-field v-model="password" :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
          :rules="[rules.required, rules.min]" :type="show1 ? 'text' : 'password'" name="input-10-1" label="Password"
          hint="At least 8 characters" counter @click:append="show1 = !show1">
        </v-text-field>
        <p>Did you <a href="" class="color-blue text-decoration-none">forget your password?</a></p>

        <div v-if="this.$route.query.user === 'agency'">
          <nuxt-link to="/register">
            <v-btn rounded color="primary" block class="mt-5">
              Login
            </v-btn>
          </nuxt-link>
        </div>
        <div v-else-if="this.$route.query.user === 'insurance'">
          <nuxt-link to="/insurance/commision-claims">
            <v-btn rounded color="primary" block class="mt-5">
              Login
            </v-btn>
          </nuxt-link>
        </div>
        <div v-else-if="this.$route.query.user === 'payer'">
          <nuxt-link to="/cca/claims">
            <v-btn rounded color="primary" block class="mt-5">
              Login
            </v-btn>
          </nuxt-link>
        </div>
        <div v-else-if="this.$route.query.user === 'agents-dash'">
          <nuxt-link to="/agencies/commision-claim">
            <v-btn rounded color="primary" block class="mt-5">
              Login
            </v-btn>
          </nuxt-link>
        </div>
      </v-card> -->
    </v-col>
  </v-row>
</template>

<style scoped>
.h-100 {
  min-height: 100vh
}
.color-blue {
  color: #3750EB;
}

.bg-blue {
  background-color: #3750EB;
}
</style>
<script>
export default {
  name: 'LoginPage',

  data() {
    return {
      email: "",
      show1: false,
      password: '',
      rules: {
        required: value => !!value || 'Required.',
        min: v => v.length >= 8 || 'Min 8 characters',
        emailMatch: () => (`The email and password you entered don't match`),
      },
    }
  },
}
</script>

