<template>
  <v-row>
    <v-col cols="12" sm="12" md="12" class="full-height-background bg-blue d-flex justify-center align-center">
      <v-card class="half-height-background bg-teal pa-10 rounded-lg">
        <h1 class="text-center color-blue">Register</h1>
        <!-- <p class="text-center py-3">Are you an insurance brokerage firm or an insurance agent?
          Are you tired of waiting for your insurance commision to get paid? You are the in the right place. By
          using our platform you dont have to wait for 45-60 days to get paid.Get paid faster, what are you waiting for
          register now?
        </p> -->
        <v-stepper v-model="e1">
          <v-stepper-header>
            <v-stepper-step :complete="e1 > 1" step="1">
              Contact Details
            </v-stepper-step>
            <v-divider></v-divider>
            <v-stepper-step :complete="e1 > 2" step="2">
              Business Details
            </v-stepper-step>
            <v-divider></v-divider>
            <v-stepper-step :complete="e1 > 3" step="3">
              Confirmation
            </v-stepper-step>


          </v-stepper-header>

          <v-stepper-items>
            <v-stepper-content step="1">

              <v-radio-group v-model="radios">
                <template v-slot:label>
                  <div>
                    <p class="font-weight-bold h6">Are you an ?</p>
                  </div>
                </template>
                <v-radio value="Insurance Brokerage Firm">
                  <template v-slot:label>
                    <div><strong class="font-weight-bold h6">Insurance Brokerage Firm</strong></div>
                  </template>
                </v-radio>
                <v-radio value="Insurance Agent">
                  <template v-slot:label>
                    <div><strong class="font-weight-bold h6">Insurance Agent</strong></div>
                  </template>
                </v-radio>
                <v-radio value="Insurance Rep Name">
                  <template v-slot:label>
                    <div><strong class="font-weight-bold h6">Insurance Rep Name</strong></div>
                  </template>
                </v-radio>
              </v-radio-group>

              <v-text-field label="What's your Brokerage/Agent/Insurance Rep Name?" filled required></v-text-field>
              <v-text-field label="What's your phone number?" required filled></v-text-field>
              <v-text-field v-model="email" label="What's your email?" required filled>
              </v-text-field>

              <v-btn color="primary" @click="e1 = 2">
                Continue
              </v-btn>

              <v-btn text>
                Cancel
              </v-btn>
            </v-stepper-content>

            <v-stepper-content step="2">
              <v-text-field label="What's your business location?" filled required></v-text-field>
              <v-text-field label="What's your IRA license no (if agent or brokerage firm)?" required filled>
              </v-text-field>
              <v-text-field
                label="What's your business registration no (if agent or brokerage firm) / id no (if sales rep) ?"
                required filled></v-text-field>
              <v-file-input filled accept="image/*"
                label="Upload your business registration no (if agent or brokerage firm) / id no (if sales rep)">
              </v-file-input>

              <v-checkbox v-model="checkbox">
                <template v-slot:label>
                  <div>
                    I agree to the
                    <v-tooltip bottom>
                      <template v-slot:activator="{ on }">
                        <a target="_blank" href="https://vuetifyjs.com" @click.stop v-on="on">
                          terms and conditions
                        </a>
                      </template>

                    </v-tooltip>

                  </div>
                </template>
              </v-checkbox>


              <v-btn color="primary" @click="e1 = 3">
                Submit
              </v-btn>

              <v-btn text @click="e1 = 1">
                Go Back
              </v-btn>
            </v-stepper-content>

            <v-stepper-content step="3">

              <h1 class="text-center color-blue">Voila !! You are done <v-icon aria-label="check all" role="img"
                  aria-hidden="false" color="#3750EB" size="32">
                  {{ icons.mdiCheckAll }}
                </v-icon>
              </h1>


              <p>We have received your registration details. Our team will verify the details you have submitted.If all
                is
                right , we will send you a link of our portal on your email for you to complete the onboarding
                process.We
                will also notify you in your email if your registration is rejected. </p>
              <p>We
                look forward to our partnership.</p>

            </v-stepper-content>
          </v-stepper-items>
        </v-stepper>
      </v-card>
    </v-col>
  </v-row>

</template>
<style scoped>
.full-height-background {
  width: 100vw;
  height: 100vh;
}

.half-height-background {
  width: 70vw;
}

.color-blue {
  color: #3750EB;
}

.bg-blue {
  background-color: #3750EB;
}

.bg-teal {
  background-color: rgb(231 240 247);
}

.v-btn.active .v-icon {
  transform: rotate(-180deg);
}
</style>
<script>
import { mdiCheckAll } from "@mdi/js";

export default {
  name: 'RegisterPage',
  data() {
    return {
      e1: 1,
      email: "",
      show1: false,
      checkbox: false,
      password: '',
      menuValue: null,
      rules: {
        required: value => !!value || 'Required.',
        min: v => v.length >= 8 || 'Min 8 characters',
        emailMatch: () => (`The email and password you entered don't match`),
      },
      icons: {
        mdiCheckAll
      }
    }
  },
}
</script>