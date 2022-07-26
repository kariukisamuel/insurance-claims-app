<template>
    <v-row no-gutters class="justify-space-between pa-5 bg-blue align-center">
        <v-col>
            <nuxt-link to="/">
                <img src="~/static/logoipsum-logo-38.svg" />
            </nuxt-link>
        </v-col>
        <v-col>
            <v-row>
                <v-col class="d-flex justify-end align-center">
                    <NuxtLink to="/agencies/commision-claim" class="d-none d-sm-flex d-sm-none d-md-flex align-center">
                        <v-icon aria-label="check all" role="img" aria-hidden="false" color="#fff" size="32"> {{
                                icons.mdiCashFast
                        }}
                        </v-icon>
                        <span class="color-white pa-3">Commision Forfeiture Claims</span>
                    </NuxtLink>
                    <NuxtLink to="/" class="text-decoration-none">
                        <v-btn color="error">
                            Logout
                        </v-btn>
                    </NuxtLink>
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
import { mdiCashFast, mdiHome } from "@mdi/js";
export default {
    name: 'insuranceMenu',
    data() {
        return {
            icons: {
                mdiCashFast,
                mdiHome
            }
        }
    },
}

</script>