<template>
    <v-card elevation="4" color="#3750EB" class="d-flex justify-space-between pa-5 align-center">
        <div>
            <img src="~/static/logoipsum-logo-38.svg" />
        </div>
        <div class="d-flex">
            <!-- <div class="text-center">
                <a href="">
                    <v-icon aria-label="check all" role="img" aria-hidden="false" color="#fff" size="32"> {{
                            icons.mdiHome
                    }}
                    </v-icon>
                    <span class="color-white pa-5">Dashboard</span>
                </a>

            </div> -->
            <div class="text-center">
                <NuxtLink to="/cca/users">
                    <v-icon aria-label="check all" role="img" aria-hidden="false" color="#fff" size="32"> {{
                            icons.mdiAccountSupervisorCircle
                    }}
                    </v-icon>
                    <span class="color-white pa-5">Users</span>
                </NuxtLink>
            </div>
            <div class="text-center">
                <NuxtLink to="/cca/utilities">
                    <v-icon aria-label="check all" role="img" aria-hidden="false" color="#fff" size="32"> {{
                            icons.mdiBorderInside
                    }}
                    </v-icon>
                    <span class="color-white pa-5">Utilities</span>
                </NuxtLink>
            </div>
            <div class="text-center">
                <NuxtLink to="/cca/claims">
                    <v-icon aria-label="check all" role="img" aria-hidden="false" color="#fff" size="32"> {{
                            icons.mdiCashFast
                    }}
                    </v-icon>
                    <span class="color-white pa-5">Commision Claims</span>
                </NuxtLink>
            </div>
        </div>




    </v-card>
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
import { mdiHome, mdiAccountSupervisorCircle, mdiBorderInside, mdiCashFast } from "@mdi/js";
export default {
    name: 'ccamenu',
    data() {
        return {
            icons: {
                mdiHome, mdiAccountSupervisorCircle, mdiBorderInside, mdiCashFast
            }
        }
    },
}

</script>