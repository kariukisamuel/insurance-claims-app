<template>
    <v-row>
        <v-col cols="12" class="full-height-background bg-blue d-flex justify-center align-center">



            <v-card class=" bg-teal pa-10 rounded-lg">
                <h2 class="text-center py-3">Commission Claims App</h2>
                <div class="d-flex justify-between">
                    <div class="pa-2">
                        <nuxt-link to="/login?user=agency" class="text-decoration-none">
                            <v-card class="mx-auto pa-5" tile>
                                <div class="d-flex justify-center">
                                    <img src="/broker.png" width="100px" />
                                </div>
                                <h4 class="text-center py-3">Agency/Brokerage Firm</h4>
                            </v-card>
                        </nuxt-link>
                    </div>

                    <div class="pa-2">
                        <nuxt-link to="/login?user=insurance" class="text-decoration-none">
                            <v-card class="mx-auto pa-5" tile>
                                <div class="d-flex justify-center">
                                    <img src="/insurance.png" width="100px" />
                                </div>
                                <h4 class="text-center py-3">Insurance Firm</h4>
                            </v-card>
                        </nuxt-link>

                    </div>

                    <div class="pa-2">
                        <nuxt-link to="/login?user=payer" class="text-decoration-none">
                            <v-card class="mx-auto pa-5" tile>
                                <div class="d-flex justify-center">
                                    <img src="/reinsurance.png" width="100px" />
                                </div>
                                <h4 class="text-center py-3">Commission Payer</h4>
                            </v-card>
                        </nuxt-link>

                    </div>

                </div>


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
    width: 40vw;
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
</style>
<script>
export default {
    name: 'IndexPage',
}
</script>