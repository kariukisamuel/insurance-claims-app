<template>
    <v-container fluid class="bg-blue h-100">
        <v-row class="d-flex justify-center align-center h-100" no-gutters>
            <v-col md="6" class="rounded-lg">
                <v-card class="indigo lighten-5 pa-10">
                    <h2 class="text-center py-3">Commission Claims App</h2>

                    <v-row>
                        <v-col class="elevation-5 ma-3 white rounded-lg px-10">
                            <nuxt-link to="/register" class="text-decoration-none pa-5">

                                <div class="d-flex justify-center">
                                    <img src="/broker.png" width="50px" />
                                </div>
                                <h4 class="text-center py-3">Agency/Brokerage Firm</h4>

                            </nuxt-link>
                        </v-col>
                      
                        <v-col class="elevation-5 ma-3 white rounded-lg px-10">
                            <nuxt-link to="/login?user=insurance" class="text-decoration-none pa-5">

                                <div class="d-flex justify-center">
                                    <img src="/insurance.png" width="50px" />
                                </div>
                                <h4 class="text-center py-3">Insurance Firm</h4>
                            </nuxt-link>
                        </v-col>
                      
                        <v-col class="elevation-5 ma-3 white rounded-lg px-10">
                            <nuxt-link to="/login?user=payer" class="text-decoration-none pa-5">

                                <div class="d-flex justify-center">
                                    <img src="/reinsurance.png" width="50px" />
                                </div>
                                <h4 class="text-center py-3">Commission Payer</h4>

                            </nuxt-link>
                        </v-col>
                    </v-row>
                    <!-- <div class="d-flex justify-between flex-wrap ">
                        <div class="pa-2 bg-teal">
                            <nuxt-link to="/register" class="text-decoration-none">
                                <v-card class="pa-5">
                                    <div class="d-flex justify-center">
                                        <img src="/broker.png" width="50px" />
                                    </div>
                                    <h4 class="text-center py-3">Agency/Brokerage</h4>
                                </v-card>
                            </nuxt-link>
                        </div>

                        <div class="pa-2">
                            <nuxt-link to="/login?user=insurance" class="text-decoration-none">
                                <v-card class="pa-5">
                                    <div class="d-flex justify-center">
                                        <img src="/insurance.png" width="50px" />
                                    </div>
                                    <h4 class="text-center py-3">Insurance Firm</h4>
                                </v-card>
                            </nuxt-link>

                        </div>

                        <div class="pa-2">
                            <nuxt-link to="/login?user=payer" class="text-decoration-none">
                                <v-card class="pa-5">
                                    <div class="d-flex justify-center">
                                        <img src="/reinsurance.png" width="50px" />
                                    </div>
                                    <h4 class="text-center py-3">Commission Settler</h4>
                                </v-card>
                            </nuxt-link>

                        </div>

                    </div> -->


                </v-card>

            </v-col>
        </v-row>
    </v-container>

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
    name: 'IndexPage',
}
</script>