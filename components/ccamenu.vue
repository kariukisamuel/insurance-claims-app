<template>
    <v-row no-gutters class="justify-space-between pa-5 bg-blue align-center">
        <v-col>
            <nuxt-link to="/">
                <img src="~/static/logoipsum-logo-38.svg" />
            </nuxt-link>
        </v-col>
        <v-col class="d-lg-block d-none">
            <v-row>
                <v-col class="d-flex justify-end align-center">
                    <NuxtLink to="/cca/claims">
                        <v-icon aria-label="check all" role="img" aria-hidden="false" color="#fff" size="32"> {{
                                icons.mdiCashFast
                        }}
                        </v-icon>
                        <span class="color-white pa-5">Commision Claims</span>
                    </NuxtLink>

                    <NuxtLink to="/cca/users">
                        <v-icon aria-label="check all" role="img" aria-hidden="false" color="#fff" size="32"> {{
                                icons.mdiAccountSupervisorCircle
                        }}
                        </v-icon>
                        <span class="color-white pa-5">Users</span>
                    </NuxtLink>
                    <NuxtLink to="/cca/utilities">
                        <v-icon aria-label="check all" role="img" aria-hidden="false" color="#fff" size="32"> {{
                                icons.mdiBorderInside
                        }}
                        </v-icon>
                        <span class="color-white pa-5">Utilities</span>
                    </NuxtLink>
                    <NuxtLink to="/" class="text-decoration-none">
                        <v-btn color="error">
                            Logout
                        </v-btn>
                    </NuxtLink>
                </v-col>
            </v-row>
        </v-col>

        <v-col class="d-lg-none ">
            <v-row>
                <v-col class="d-flex justify-end">
                    <v-menu offset-y>
                        <template v-slot:activator="{ on, attrs }">
                            <v-app-bar-nav-icon color="white" v-bind="attrs" v-on="on"></v-app-bar-nav-icon>
                        </template>

                        <v-list>
                            <v-list-item>
                                <v-list-item-title>
                                    <NuxtLink to="/cca/claims" class="text-decoration-none">
                                        <v-icon aria-label="check all" role="img" aria-hidden="false" color="#3750EB"
                                            size="32"> {{
                                                    icons.mdiCashFast
                                            }}
                                        </v-icon>
                                        <span class="color-blue pa-5">Commision Claims</span>
                                    </NuxtLink>
                                </v-list-item-title>
                            </v-list-item>
                            <v-list-item>
                                <v-list-item-title>
                                    <NuxtLink to="/cca/users" class="text-decoration-none">
                                        <v-icon aria-label="check all" role="img" aria-hidden="false" color="#3750EB"
                                            size="32"> {{
                                                    icons.mdiAccountSupervisorCircle
                                            }}
                                        </v-icon>
                                        <span class="color-blue pa-5">Users</span>
                                    </NuxtLink>
                                </v-list-item-title>
                            </v-list-item>
                            <v-list-item>
                                <v-list-item-title>
                                    <NuxtLink to="/cca/utilities" class="text-decoration-none">
                                        <v-icon aria-label="check all" role="img" aria-hidden="false" color="#3750EB"
                                            size="32"> {{
                                                      icons.mdiBorderInside
                                            }}
                                        </v-icon>
                                        <span class="color-blue pa-5">Utilities</span>
                                    </NuxtLink>
                                </v-list-item-title>
                            </v-list-item>
                            <v-list-item>
                                <v-list-item-title>
                                    <NuxtLink to="/" class="text-decoration-none">
                                        <v-icon aria-label="check all" role="img" aria-hidden="false" color="red"
                                            size="32"> {{
                                                    icons.mdiLogout 
                                            }}
                                        </v-icon>
                                        <span class="pa-5 red--text text--lighten-1">Logout</span>
                                    </NuxtLink>
                                </v-list-item-title>
                            </v-list-item>

                        </v-list>
                    </v-menu>

                </v-col>
            </v-row>
        </v-col>

    </v-row>
</template>
<style>
.color-blue {
    color: #3750EB;
}

.color-white {
    color: #ffffff
}

.bg-blue {
    background-color: #3750EB;
}

.bg-teal {
    background-color: rgb(231 240 247);
}
</style>
<script>
import { mdiHome, mdiAccountSupervisorCircle, mdiBorderInside, mdiCashFast,mdiLogout } from "@mdi/js";
export default {
    name: 'ccamenu',
    data() {
        return {
            icons: {
                mdiHome, mdiAccountSupervisorCircle, mdiBorderInside, mdiCashFast,mdiLogout
            }
        }
    },
}

</script>