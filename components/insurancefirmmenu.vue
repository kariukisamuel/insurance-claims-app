<template>
    <v-toolbar elevation="4" color="#3750EB" class="d-flex justify-space-between ">
        <div>
            <img src="~/static/logoipsum-logo-38.svg" />
        </div>
        <div class="d-flex">
            <div class="text-center">
                <a href="">
                    <v-icon aria-label="check all" role="img" aria-hidden="false" color="#fff" size="32"> {{
                            icons.mdiHome
                    }}
                    </v-icon>
                    <span class="color-white pa-5">Dashboard</span>
                </a>

            </div>
            <div class="text-center">
                <NuxtLink to="/insurance/commision-claims">
                    <v-icon aria-label="check all" role="img" aria-hidden="false" color="#fff" size="32"> {{
                            icons.mdiCashFast
                    }}
                    </v-icon>
                    <span class="color-white pa-5">Commision Forfeiture Claims</span>
                </NuxtLink>
            </div>

        </div>
    </v-toolbar>
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
import { mdiCashFast } from "@mdi/js";
export default {
    name: 'insuranceMenu',
    data() {
        return {
            icons: {
               mdiCashFast
            }
        }
    },
}

</script>