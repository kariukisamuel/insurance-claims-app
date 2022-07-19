<template>
    <v-container fluid class="pa-0 bg-teal">
        <v-row no-gutters>
            <v-col cols="12">
                <ccamenu />
            </v-col>
        </v-row>
        <v-row no-gutters class="pa-10">
            <v-col cols="12">
                <v-card>
                    <v-tabs fixed-tabs background-color="#3750EB" dark v-model="tabs">
                        <v-tab href="#tab-1">All</v-tab>
                        <v-tab href="#tab-2">Approved By Insurance Firms</v-tab>
                        <v-tab href="#tab-3">Disapproved By Insurance Firms</v-tab>
                        <v-tab href="#tab-4">Approved For Payment</v-tab>
                        <v-tab href="#tab-5">Disapproved For Payment</v-tab>



                    </v-tabs>
                    <v-tabs-items v-model="tabs">
                        <v-tab-item value="tab-1">
                            <v-card flat>
                                <v-card-title class="d-flex justify-end">
                                    <v-btn color="primary" dark v-bind="attrs" v-on="on">
                                        <v-icon left>
                                            {{ icons.mdiMicrosoftExcel }}
                                        </v-icon>
                                        Export Excel Report
                                    </v-btn>
                                </v-card-title>

                                <v-card-title>
                                    <v-text-field v-model="search" append-icon="mdi-magnify" label="Search" single-line
                                        hide-details></v-text-field>
                                </v-card-title>
                                <v-card-text>
                                    <v-data-table :headers="claims.headers" :items="claims.details" :items-per-page="10"
                                        class="elevation-1">
                                        <template v-slot:item.status="{ item }">
                                            <v-chip :color="getClaimStatus(item.status)" dark v-if="item.status === 0">
                                                Pending Insurance Approval
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 1">
                                                Approved By Insurance
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 2">
                                                Rejected By Insurance
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 3">
                                                Approved For Payment
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 4">
                                                Payment Rejected
                                            </v-chip>

                                        </template>
                                        <template v-slot:item.actions="{ item }">
                                            <v-icon small class="mr-2" @click="editPolicy(item)">
                                                {{ icons.mdiDotsVertical }}
                                            </v-icon>
                                        </template>
                                    </v-data-table>
                                </v-card-text>
                            </v-card>
                        </v-tab-item>
                        <v-tab-item value="tab-2">

                            <v-card flat>
                                <v-card-title class="d-flex justify-end">
                                    <v-btn color="primary" dark v-bind="attrs" v-on="on">
                                        <v-icon left>
                                            {{ icons.mdiMicrosoftExcel }}
                                        </v-icon>
                                        Export Excel Report
                                    </v-btn>
                                </v-card-title>

                                <v-card-title>
                                    <v-text-field v-model="search" append-icon="mdi-magnify" label="Search" single-line
                                        hide-details></v-text-field>
                                </v-card-title>
                                <v-card-text>
                                    <v-data-table :headers="claims.headers" :items="insuranceApproved"
                                        :items-per-page="10" class="elevation-1">
                                        <template v-slot:item.status="{ item }">
                                            <v-chip :color="getClaimStatus(item.status)" dark v-if="item.status === 0">
                                                Pending Insurance Approval
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 1">
                                                Approved By Insurance
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 2">
                                                Rejected By Insurance
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 3">
                                                Approved For Payment
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 4">
                                                Payment Rejected
                                            </v-chip>

                                        </template>
                                        <template v-slot:item.actions="{ item }">
                                            <v-icon small class="mr-2" @click="editPolicy(item)">
                                                {{ icons.mdiDotsVertical }}
                                            </v-icon>
                                        </template>
                                    </v-data-table>
                                </v-card-text>
                            </v-card>
                        </v-tab-item>
                        <v-tab-item value="tab-3">
                            <v-card flat>
                                <v-card-title class="d-flex justify-end">
                                    <v-btn color="primary" dark v-bind="attrs" v-on="on">
                                        <v-icon left>
                                            {{ icons.mdiMicrosoftExcel }}
                                        </v-icon>
                                        Export Excel Report
                                    </v-btn>
                                </v-card-title>

                                <v-card-title>
                                    <v-text-field v-model="search" append-icon="mdi-magnify" label="Search" single-line
                                        hide-details></v-text-field>
                                </v-card-title>
                                <v-card-text>
                                    <v-data-table :headers="claims.headers" :items="insuranceDisapproved"
                                        :items-per-page="10" class="elevation-1">
                                        <template v-slot:item.status="{ item }">
                                            <v-chip :color="getClaimStatus(item.status)" dark v-if="item.status === 0">
                                                Pending Insurance Approval
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 1">
                                                Approved By Insurance
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 2">
                                                Rejected By Insurance
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 3">
                                                Approved For Payment
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 4">
                                                Payment Rejected
                                            </v-chip>

                                        </template>
                                        <template v-slot:item.actions="{ item }">
                                            <v-icon small class="mr-2" @click="editPolicy(item)">
                                                {{ icons.mdiDotsVertical }}
                                            </v-icon>
                                        </template>
                                    </v-data-table>
                                </v-card-text>
                            </v-card>
                        </v-tab-item>
                        <v-tab-item value="tab-4">
                            <v-card flat>
                                <v-card-title class="d-flex justify-end">
                                    <v-btn color="primary" dark v-bind="attrs" v-on="on">
                                        <v-icon left>
                                            {{ icons.mdiMicrosoftExcel }}
                                        </v-icon>
                                        Export Excel Report
                                    </v-btn>
                                </v-card-title>

                                <v-card-title>
                                    <v-text-field v-model="search" append-icon="mdi-magnify" label="Search" single-line
                                        hide-details></v-text-field>
                                </v-card-title>
                                <v-card-text>
                                    <v-data-table :headers="claims.headers" :items="cfaApproved" :items-per-page="10"
                                        class="elevation-1">
                                        <template v-slot:item.status="{ item }">
                                            <v-chip :color="getClaimStatus(item.status)" dark v-if="item.status === 0">
                                                Pending Insurance Approval
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 1">
                                                Approved By Insurance
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 2">
                                                Rejected By Insurance
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 3">
                                                Approved For Payment
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 4">
                                                Payment Rejected
                                            </v-chip>

                                        </template>
                                        <template v-slot:item.actions="{ item }">
                                            <v-icon small class="mr-2" @click="editPolicy(item)">
                                                {{ icons.mdiDotsVertical }}
                                            </v-icon>
                                        </template>
                                    </v-data-table>
                                </v-card-text>
                            </v-card>
                        </v-tab-item>
                        <v-tab-item value="tab-5">
                            <v-card flat>
                                <v-card-title class="d-flex justify-end">
                                    <v-btn color="primary" dark v-bind="attrs" v-on="on">
                                        <v-icon left>
                                            {{ icons.mdiMicrosoftExcel }}
                                        </v-icon>
                                        Export Excel Report
                                    </v-btn>
                                </v-card-title>

                                <v-card-title>
                                    <v-text-field v-model="search" append-icon="mdi-magnify" label="Search" single-line
                                        hide-details></v-text-field>
                                </v-card-title>

                                <v-card-text>
                                    <v-data-table :headers="claims.headers" :items="cfaDisapproved" :items-per-page="10"
                                        class="elevation-1">
                                        <template v-slot:item.status="{ item }">
                                            <v-chip :color="getClaimStatus(item.status)" dark v-if="item.status === 0">
                                                Pending Insurance Approval
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 1">
                                                Approved By Insurance
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 2">
                                                Rejected By Insurance
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 3">
                                                Approved For Payment
                                            </v-chip>
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 4">
                                                Payment Rejected
                                            </v-chip>

                                        </template>
                                        <template v-slot:item.actions="{ item }">
                                            <v-icon small class="mr-2" @click="editPolicy(item)">
                                                {{ icons.mdiDotsVertical }}
                                            </v-icon>
                                        </template>
                                    </v-data-table>
                                </v-card-text>
                            </v-card>
                        </v-tab-item>

                    </v-tabs-items>
                </v-card>

                <v-dialog v-model="dialogEditClaim" hide-overlay transition="dialog-bottom-transition" fullscreen>
                    <v-card>
                        <v-toolbar dark color="primary">
                            <v-btn icon dark @click="dialogEditClaim = false">
                                <v-icon>mdi-close</v-icon>
                            </v-btn>
                            <v-toolbar-title>Commission Claim Details</v-toolbar-title>
                        </v-toolbar>
                        <v-card-text>
                            <v-container>
                                <v-row class="py-4">
                                    <v-expansion-panels>
                                        <v-expansion-panel key="1">
                                            <v-expansion-panel-header>
                                                Agency/Brokerage Name
                                            </v-expansion-panel-header>
                                            <v-expansion-panel-content>
                                                {{ editedClaims.name }}
                                            </v-expansion-panel-content>
                                        </v-expansion-panel>
                                        <v-expansion-panel key="2">
                                            <v-expansion-panel-header>
                                                Agency/Brokerage Phone Number
                                            </v-expansion-panel-header>
                                            <v-expansion-panel-content>
                                                {{ editedClaims.phoneNumber }}
                                            </v-expansion-panel-content>
                                        </v-expansion-panel>
                                        <v-expansion-panel key="3">
                                            <v-expansion-panel-header>
                                                Location
                                            </v-expansion-panel-header>
                                            <v-expansion-panel-content>
                                                {{ editedClaims.location }}
                                            </v-expansion-panel-content>
                                        </v-expansion-panel>
                                        <v-expansion-panel key="3">
                                            <v-expansion-panel-header>
                                                Insurance Company
                                            </v-expansion-panel-header>
                                            <v-expansion-panel-content>
                                                {{ editedClaims.insuranceCompany }}
                                            </v-expansion-panel-content>
                                        </v-expansion-panel>
                                        <v-expansion-panel key="4">
                                            <v-expansion-panel-header>
                                                Policy Type
                                            </v-expansion-panel-header>
                                            <v-expansion-panel-content>
                                                {{ editedClaims.policyType }}
                                            </v-expansion-panel-content>
                                        </v-expansion-panel>
                                        <v-expansion-panel key="5">
                                            <v-expansion-panel-header>
                                                Policy No
                                            </v-expansion-panel-header>
                                            <v-expansion-panel-content>
                                                {{ editedClaims.policyNo }}
                                            </v-expansion-panel-content>
                                        </v-expansion-panel>
                                        <v-expansion-panel key="5">
                                            <v-expansion-panel-header>
                                                Policy Value
                                            </v-expansion-panel-header>
                                            <v-expansion-panel-content>
                                                {{ editedClaims.policyValue }}
                                            </v-expansion-panel-content>
                                        </v-expansion-panel>
                                        <v-expansion-panel key="5">
                                            <v-expansion-panel-header>
                                                Commission Value
                                            </v-expansion-panel-header>
                                            <v-expansion-panel-content>
                                                {{ editedClaims.commisionValue }}
                                            </v-expansion-panel-content>
                                        </v-expansion-panel>

                                        <v-expansion-panel key="6">
                                            <v-expansion-panel-header>
                                                Commission Payment Status
                                            </v-expansion-panel-header>
                                            <v-expansion-panel-content>
                                                {{ editedClaims.status }}
                                            </v-expansion-panel-content>
                                        </v-expansion-panel>

                                        <v-expansion-panel key="6">
                                            <v-expansion-panel-header>
                                                Uploads
                                            </v-expansion-panel-header>
                                            <v-expansion-panel-content>
                                                <img src="https://via.placeholder.com/500" />
                                            </v-expansion-panel-content>
                                        </v-expansion-panel>
                                    </v-expansion-panels>

                                </v-row>
                                <v-row>
                                    <v-col cols="12">
                                        <v-btn tile color="primary">
                                            <v-icon left>
                                                {{ icons.mdiAccountCheck }}
                                            </v-icon>
                                            Approve Payment
                                        </v-btn>
                                        <v-btn tile color="error">
                                            <v-icon left>
                                                {{ icons.mdiAccountCancel }}
                                            </v-icon>
                                            Disapprove Payment
                                        </v-btn>
                                    </v-col>
                                </v-row>
                            </v-container>
                        </v-card-text>


                    </v-card>

                </v-dialog>


            </v-col>
        </v-row>

    </v-container>

</template>
<script>
import { mdiDotsVertical, mdiMicrosoftExcel } from "@mdi/js";

export default {
    name: "CcaClaimsPage",
    data() {
        return {
            tabs: null,
            icons: { mdiDotsVertical, mdiMicrosoftExcel },
            claims: {
                headers: [
                    {
                        text: 'Agent/Brokerage Name',
                        align: 'start',
                        sortable: false,
                        value: 'name',
                    },
                    { text: 'Agent/Brokerage Phone Number', value: 'phoneNumber' },
                    { text: 'Location', value: 'location' },
                    { text: 'Claim Status', value: 'status' },
                    { text: 'Insurance Company', value: 'insuranceCompany' },
                    { text: 'Policy Type', value: 'policyType' },
                    { text: 'Policy Number', value: 'policyNo' },
                    { text: 'Policy Value', value: 'policyValue' },
                    { text: 'Commission Value', value: 'commisionValue' },
                    { text: 'Actions', value: 'actions' },

                ],
                details: [
                    {
                        name: 'Mwangaza Roshanee Agency',
                        phoneNumber: "0110 101 102",
                        location: "Ruiru",
                        status: 0,
                        insuranceCompany: "Jubilee Insurance",
                        policyType: "Medical Insurance",
                        policyNo: "001",
                        policyValue: "4000000",
                        commisionValue: "400000"
                    },
                    {
                        name: 'Mwangaza Roshanee Agency',
                        phoneNumber: "0110 101 102",
                        location: "Ruiru",
                        status: 1,
                        insuranceCompany: "Jubilee Insurance",
                        policyType: "Medical Insurance",
                        policyNo: "001",
                        policyValue: "4000000",
                        commisionValue: "400000"
                    },
                    {
                        name: 'Mwangaza Roshanee Agency',
                        phoneNumber: "0110 101 102",
                        location: "Ruiru",
                        status: 2,
                        insuranceCompany: "Jubilee Insurance",
                        policyType: "Medical Insurance",
                        policyNo: "001",
                        policyValue: "4000000",
                        commisionValue: "400000"
                    },
                    {
                        name: 'Mwangaza Roshanee Agency',
                        phoneNumber: "0110 101 102",
                        location: "Ruiru",
                        status: 3,
                        insuranceCompany: "Jubilee Insurance",
                        policyType: "Medical Insurance",
                        policyNo: "001",
                        policyValue: "4000000",
                        commisionValue: "400000"
                    },
                    {
                        name: 'Mwangaza Roshanee Agency',
                        phoneNumber: "0110 101 102",
                        location: "Ruiru",
                        status: 4,
                        insuranceCompany: "Jubilee Insurance",
                        policyType: "Medical Insurance",
                        policyNo: "001",
                        policyValue: "4000000",
                        commisionValue: "400000"
                    },
                    {
                        name: 'Mwangaza Roshanee Agency',
                        phoneNumber: "0110 101 102",
                        location: "Ruiru",
                        status: 0,
                        insuranceCompany: "Jubilee Insurance",
                        policyType: "Medical Insurance",
                        policyNo: "001",
                        policyValue: "4000000",
                        commisionValue: "400000"
                    },
                    {
                        name: 'Mwangaza Roshanee Agency',
                        phoneNumber: "0110 101 102",
                        location: "Ruiru",
                        status: 1,
                        insuranceCompany: "Jubilee Insurance",
                        policyType: "Medical Insurance",
                        policyNo: "001",
                        policyValue: "4000000",
                        commisionValue: "400000"
                    },
                    {
                        name: 'Mwangaza Roshanee Agency',
                        phoneNumber: "0110 101 102",
                        location: "Ruiru",
                        status: 2,
                        insuranceCompany: "Jubilee Insurance",
                        policyType: "Medical Insurance",
                        policyNo: "001",
                        policyValue: "4000000",
                        commisionValue: "400000"
                    },
                    {
                        name: 'Mwangaza Roshanee Agency',
                        phoneNumber: "0110 101 102",
                        location: "Ruiru",
                        status: 3,
                        insuranceCompany: "Jubilee Insurance",
                        policyType: "Medical Insurance",
                        policyNo: "001",
                        policyValue: "4000000",
                        commisionValue: "400000"
                    },
                    {
                        name: 'Mwangaza Roshanee Agency',
                        phoneNumber: "0110 101 102",
                        location: "Ruiru",
                        status: 4,
                        insuranceCompany: "Jubilee Insurance",
                        policyType: "Medical Insurance",
                        policyNo: "001",
                        policyValue: "4000000",
                        commisionValue: "400000"
                    },
                ]
            },
            editedPolicyIndex: '',
            editedClaims: {
                name: '',
                phoneNumber: "",
                location: "",
                status: 0,
                insuranceCompany: "",
                policyType: " ",
                policyNo: "",
                policyValue: "",
                commisionValue: ""
            },
            dialogEditClaim: false
        }
    },
    computed: {
        insuranceApproved() {
            if (this.claims.details.length > 0) {
                return this.claims.details.filter(claim => claim.status === 1)
            }
        },
        insuranceDisapproved() {
            if (this.claims.details.length > 0) {
                return this.claims.details.filter(claim => claim.status === 2)
            }
        },
        cfaApproved() {
            if (this.claims.details.length > 0) {
                return this.claims.details.filter(claim => claim.status === 3)
            }
        },
        cfaDisapproved() {
            if (this.claims.details.length > 0) {
                return this.claims.details.filter(claim => claim.status === 4)
            }
        }
    },
    methods: {
        getClaimStatus(status) {

            if (status === 0) return 'orange'
            else if (status === 1) return 'green'
            else if (status === 2) return 'red'
            else if (status === 3) return 'blue'
            else return 'black'
        },
        editPolicy(item) {
            this.editedFirmIndex = this.claims.details.indexOf(item)
            this.editedClaims = Object.assign({}, item)
            this.dialogEditClaim = true
        },
    },
}
</script>