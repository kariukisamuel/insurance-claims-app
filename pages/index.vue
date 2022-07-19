<template>
  <v-row>
    <v-col cols="12" sm="12" md="12" class="full-height-background bg-blue d-flex justify-center align-center" >
      <v-card class="half-height-background bg-teal pa-10 rounded-lg">
        <h1 class="text-center color-blue">Login</h1>
        <p class="text-center py-3">Welcome to the Insurance Commision Claims App.</p>
        

        <v-text-field v-model="email" color="purple darken-2" label="Email" required>
        </v-text-field>
        <v-text-field v-model="password" :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
          :rules="[rules.required, rules.min]" :type="show1 ? 'text' : 'password'" name="input-10-1"
          label="Password" hint="At least 8 characters" counter @click:append="show1 = !show1">
        </v-text-field>
        <p>Did you <a href="" class="color-blue text-decoration-none">forget your password?</a></p>
        <v-btn rounded color="primary" block class="mt-5">
          Login
        </v-btn>

      </v-card>
    </v-col>
  </v-row>
</template>

<style>
.full-height-background {
  width: 100vw;
  height: 100vh;
}

.half-height-background {
  width: 40vw;
}
.color-blue{
    color: #3750EB;
}

.bg-blue {
  background-color: #3750EB;
}

.bg-teal {
   background-color: rgb(231 240 247);
}
</style>
<script>
export default {
  name: 'IndexPage',
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

