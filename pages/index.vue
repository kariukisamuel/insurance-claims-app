<template>
    <v-row>
        <v-col cols="12" class="full-height-background bg-blue d-flex justify-center align-center">



            <v-card class=" bg-teal pa-10 rounded-lg">
                <h2 class="text-center py-3">System Pages</h2>
                <div class="d-flex justify-between">
                    <div class="pa-2">
                        <v-card class="mx-auto pa-5" tile>
                            <h4 class="text-center py-3">Agency/Brokerage Pages</h4>
                            <v-list-item>
                                <v-list-item-content>
                                    <nuxt-link to="/register">
                                        <v-list-item-title>Register</v-list-item-title>
                                    </nuxt-link>

                                </v-list-item-content>
                            </v-list-item>
                            <v-list-item>
                                <v-list-item-content>
                                    <nuxt-link to="/login">
                                        <v-list-item-title>Login</v-list-item-title>
                                    </nuxt-link>

                                </v-list-item-content>
                            </v-list-item>
                            <v-list-item>
                                <v-list-item-content>
                                    <nuxt-link to="/agencies/commision-claim">
                                        <v-list-item-title>Dashboard</v-list-item-title>
                                    </nuxt-link>

                                </v-list-item-content>
                            </v-list-item>

                        </v-card>
                    </div>

                    <div class="pa-2">
                        <v-card class="mx-auto pa-5" tile>
                            <h4 class="text-center py-3">Insurance Firm Pages</h4>
                            <v-list-item>
                                <v-list-item-content>
                                    <nuxt-link to="/login">
                                        <v-list-item-title>Login</v-list-item-title>
                                    </nuxt-link>

                                </v-list-item-content>
                            </v-list-item>
                            <v-list-item>
                                <v-list-item-content>
                                    <nuxt-link to="/insurance/commision-claims">
                                        <v-list-item-title>Dashboard</v-list-item-title>
                                    </nuxt-link>

                                </v-list-item-content>
                            </v-list-item>

                        </v-card>
                    </div>

                    <div class="pa-2">
                        <v-card class="mx-auto pa-5" tile>
                            <h4 class="text-center py-3">Commision Settler Pages</h4>
                            <v-list-item>
                                <v-list-item-content>
                                    <nuxt-link to="/login">
                                        <v-list-item-title>Login</v-list-item-title>
                                    </nuxt-link>

                                </v-list-item-content>
                            </v-list-item>
                            <v-list-item>
                                <v-list-item-content>
                                    <nuxt-link to="/cca/claims">
                                        <v-list-item-title>Commision Claims</v-list-item-title>
                                    </nuxt-link>

                                </v-list-item-content>
                            </v-list-item>
                            <v-list-item>
                                <v-list-item-content>
                                    <nuxt-link to="/cca/users">
                                        <v-list-item-title>Users</v-list-item-title>
                                    </nuxt-link>

                                </v-list-item-content>
                            </v-list-item>
                            <v-list-item>
                                <v-list-item-content>
                                    <nuxt-link to="/cca/claims">
                                        <v-list-item-title>Utilities</v-list-item-title>
                                    </nuxt-link>

                                </v-list-item-content>
                            </v-list-item>

                        </v-card>
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