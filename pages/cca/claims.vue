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
                    <v-tabs fixed-tabs background-color="#3750EB" dark show-arrows v-model="tabs">
                        <v-tab href="#tab-1">All</v-tab>
                        <v-tab href="#tab-3">Disapproved By Insurance</v-tab>
                        <v-tab href="#tab-2">Approved By Insurance</v-tab>
                        <v-tab href="#tab-5">Disapproved Payment</v-tab>
                        <v-tab href="#tab-4">Approved Payment</v-tab>
                        <v-tab href="#tab-6">Paid Out</v-tab>
                    </v-tabs>
                    <v-tabs-items v-model="tabs">
                        <v-tab-item value="tab-1">
                            <v-card flat>
                                <v-card-title class="d-flex justify-end">
                                    <template>
                                        <v-row>
                                            <v-col cols="12" sm="6" md="4">
                                                <v-menu ref="menu1" v-model="menu1" :close-on-content-click="false"
                                                    :return-value.sync="date" transition="scale-transition" offset-y
                                                    min-width="auto">
                                                    <template v-slot:activator="{ on, attrs }">
                                                        <v-text-field v-model="date" label="Choose Date Range"
                                                            prepend-icon="mdi-calendar" readonly v-bind="attrs"
                                                            v-on="on"></v-text-field>
                                                    </template>
                                                    <v-date-picker v-model="date" no-title scrollable>
                                                        <v-spacer></v-spacer>
                                                        <v-btn text color="primary" @click="menu = false">
                                                            Cancel
                                                        </v-btn>
                                                        <v-btn text color="primary" @click="$refs.menu.save(date)">
                                                            OK
                                                        </v-btn>
                                                    </v-date-picker>
                                                </v-menu>
                                            </v-col>
                                        </v-row>
                                    </template>
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
                                    <template>
                                        <v-row>
                                            <v-col cols="12" sm="6" md="4">
                                                <v-menu ref="menu2" v-model="menu2" :close-on-content-click="false"
                                                    :return-value.sync="date" transition="scale-transition" offset-y
                                                    min-width="auto">
                                                    <template v-slot:activator="{ on, attrs }">
                                                        <v-text-field v-model="date" label="Choose Date Range"
                                                            prepend-icon="mdi-calendar" readonly v-bind="attrs"
                                                            v-on="on"></v-text-field>
                                                    </template>
                                                    <v-date-picker v-model="date" no-title scrollable>
                                                        <v-spacer></v-spacer>
                                                        <v-btn text color="primary" @click="menu = false">
                                                            Cancel
                                                        </v-btn>
                                                        <v-btn text color="primary" @click="$refs.menu.save(date)">
                                                            OK
                                                        </v-btn>
                                                    </v-date-picker>
                                                </v-menu>
                                            </v-col>
                                        </v-row>
                                    </template>
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
                                    <template>
                                        <v-row>
                                            <v-col cols="12" sm="6" md="4">
                                                <v-menu ref="menu3" v-model="menu3" :close-on-content-click="false"
                                                    :return-value.sync="date" transition="scale-transition" offset-y
                                                    min-width="auto">
                                                    <template v-slot:activator="{ on, attrs }">
                                                        <v-text-field v-model="date" label="Choose Date Range"
                                                            prepend-icon="mdi-calendar" readonly v-bind="attrs"
                                                            v-on="on"></v-text-field>
                                                    </template>
                                                    <v-date-picker v-model="date" no-title scrollable>
                                                        <v-spacer></v-spacer>
                                                        <v-btn text color="primary" @click="menu = false">
                                                            Cancel
                                                        </v-btn>
                                                        <v-btn text color="primary" @click="$refs.menu.save(date)">
                                                            OK
                                                        </v-btn>
                                                    </v-date-picker>
                                                </v-menu>
                                            </v-col>
                                        </v-row>
                                    </template>
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
                                    <template>
                                        <v-row>
                                            <v-col cols="12" sm="6" md="4">
                                                <v-menu ref="menu4" v-model="menu4" :close-on-content-click="false"
                                                    :return-value.sync="date" transition="scale-transition" offset-y
                                                    min-width="auto">
                                                    <template v-slot:activator="{ on, attrs }">
                                                        <v-text-field v-model="date" label="Choose Date Range"
                                                            prepend-icon="mdi-calendar" readonly v-bind="attrs"
                                                            v-on="on"></v-text-field>
                                                    </template>
                                                    <v-date-picker v-model="date" no-title scrollable>
                                                        <v-spacer></v-spacer>
                                                        <v-btn text color="primary" @click="menu = false">
                                                            Cancel
                                                        </v-btn>
                                                        <v-btn text color="primary" @click="$refs.menu.save(date)">
                                                            OK
                                                        </v-btn>
                                                    </v-date-picker>
                                                </v-menu>
                                            </v-col>
                                        </v-row>
                                    </template>
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
                                    <template>
                                        <v-row>
                                            <v-col cols="12" sm="6" md="4">
                                                <v-menu ref="menu5" v-model="menu5" :close-on-content-click="false"
                                                    :return-value.sync="date" transition="scale-transition" offset-y
                                                    min-width="auto">
                                                    <template v-slot:activator="{ on, attrs }">
                                                        <v-text-field v-model="date" label="Choose Date Range"
                                                            prepend-icon="mdi-calendar" readonly v-bind="attrs"
                                                            v-on="on"></v-text-field>
                                                    </template>
                                                    <v-date-picker v-model="date" no-title scrollable>
                                                        <v-spacer></v-spacer>
                                                        <v-btn text color="primary" @click="menu = false">
                                                            Cancel
                                                        </v-btn>
                                                        <v-btn text color="primary" @click="$refs.menu.save(date)">
                                                            OK
                                                        </v-btn>
                                                    </v-date-picker>
                                                </v-menu>
                                            </v-col>
                                        </v-row>
                                    </template>
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
                        <v-tab-item value="tab-6">
                            <v-card flat>
                                <v-card-title class="d-flex justify-end">

                                    <template>
                                        <v-row>
                                            <v-col cols="12" sm="6" md="4">
                                                <v-menu ref="menu6" v-model="menu6" :close-on-content-click="false"
                                                    :return-value.sync="date" transition="scale-transition" offset-y
                                                    min-width="auto">
                                                    <template v-slot:activator="{ on, attrs }">
                                                        <v-text-field v-model="date" label="Choose Date Range"
                                                            prepend-icon="mdi-calendar" readonly v-bind="attrs"
                                                            v-on="on"></v-text-field>
                                                    </template>
                                                    <v-date-picker v-model="date" no-title scrollable>
                                                        <v-spacer></v-spacer>
                                                        <v-btn text color="primary" @click="menu = false">
                                                            Cancel
                                                        </v-btn>
                                                        <v-btn text color="primary" @click="$refs.menu.save(date)">
                                                            OK
                                                        </v-btn>
                                                    </v-date-picker>
                                                </v-menu>
                                            </v-col>
                                        </v-row>
                                    </template>
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
                                    <v-data-table :headers="claims.headers" :items="paid" :items-per-page="10"
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
                                            <v-chip :color="getClaimStatus(item.status)" dark
                                                v-else-if="item.status === 5">
                                                Paid Out
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
                                    <v-col cols="12" class="d-flex pa-0">
                                        <table>
                                            <tr>
                                                <td class="px-5">Agency/Brokerage Name :</td>
                                                <td class="px-5">{{ editedClaims.name }}</td>
                                            </tr>
                                            <tr>
                                                <td class="px-5">Agency/Brokerage Phone Number :</td>
                                                <td class="px-5">{{ editedClaims.phoneNumber }}</td>
                                            </tr>
                                            <tr>
                                                <td class="px-5">Location:</td>
                                                <td class="px-5">{{ editedClaims.location }}</td>
                                            </tr>
                                            <tr>
                                                <td class="px-5">Insurance Company:</td>
                                                <td class="px-5">{{ editedClaims.insuranceCompany }}</td>
                                            </tr>
                                            <tr>
                                                <td class="px-5">Policy Type :</td>
                                                <td class="px-5">{{ editedClaims.policyType }}</td>
                                            </tr>
                                            <tr>
                                                <td class="px-5">Policy No :</td>
                                                <td class="px-5">{{ editedClaims.policyNo }}</td>
                                            </tr>
                                            <tr>
                                                <td class="px-5">Policy Value :</td>
                                                <td class="px-5">{{ editedClaims.policyValue }}</td>
                                            </tr>

                                            <tr>
                                                <td class="px-5">Policy Copy :</td>
                                                <td class="px-5">
                                                    <a href="/policy.pdf" download="" target="_blank">Policy
                                                        Copy PDF</a>
                                                </td>
                                            </tr>
                                            <tr>
                                                <td class="px-5">Invoice No :</td>
                                                <td class="px-5">{{ editedClaims.invoiceNo }}</td>
                                            </tr>

                                            <tr>
                                                <td class="px-5">Invoice Copy :</td>
                                                <td class="px-5">
                                                    <a href="/invoice.pdf" download="" target="_blank">Invoice
                                                        Copy PDF</a>
                                                </td>
                                            </tr>
                                            <tr>
                                                <td class="px-5">Commission Value :</td>
                                                <td class="px-5">{{ editedClaims.commisionValue }}</td>
                                            </tr>
                                            <tr>
                                                <td class="px-5">Commission Payment Status :</td>
                                                <td class="px-5 text--orange" v-if="editedClaims.status === 0">
                                                    <p class="text--orange ma-0">Pending Insurance Approval</p>
                                                </td>
                                                <td class="px-5 text--green" v-else-if="editedClaims.status === 1">
                                                    Approved By Insurance
                                                </td>
                                                <td class="px-5 text--red" v-else-if="editedClaims.status === 2">
                                                    Rejected By Insurance
                                                </td>
                                                <td class="px-5 text--blue" v-else-if="editedClaims.status === 3">
                                                    Approved For Payment
                                                </td>
                                                <td class="px-5 text--black" v-else-if="editedClaims.status === 4">
                                                    Payment Rejected
                                                </td>
                                                <td class="px-5 text--black" v-else-if="editedClaims.status === 5">
                                                    Paid Out
                                                </td>
                                            </tr>

                                        </table>
                                    </v-col>
                                </v-row>
                                <v-row>
                                    <v-col cols="12" v-if="editedClaims.status === 1">
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
                                    <v-col cols="12" v-if="editedClaims.status === 4">
                                        <v-btn tile color="primary">
                                            <v-icon left>
                                                {{ icons.mdiAccountCheck }}
                                            </v-icon>
                                            Reapprove For Payment
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
<script scoped>
import { mdiDotsVertical, mdiMicrosoftExcel } from "@mdi/js";

export default {
    name: "CcaClaimsPage",
    data() {
        return {

            date: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
            menu1: false,
            menu2: false,
            menu3: false,
            menu4: false,
            menu5: false,
            menu6: false,
            modal: false,

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
                    { text: 'Invoice Number', value: 'invoiceNo' },
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
                        commisionValue: "400000",
                        invoiceNo: "002"
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
                        commisionValue: "400000",
                        invoiceNo: "002"
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
                        commisionValue: "400000",
                        invoiceNo: "002"
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
                        commisionValue: "400000",
                        invoiceNo: "002"
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
                        commisionValue: "400000",
                        invoiceNo: "002"
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
                        commisionValue: "400000",
                        invoiceNo: "002"
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
                        commisionValue: "400000",
                        invoiceNo: "002"
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
                        commisionValue: "400000",
                        invoiceNo: "002"
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
                        commisionValue: "400000",
                        invoiceNo: "002"
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
                        commisionValue: "400000",
                        invoiceNo: "002"
                    },
                    {
                        name: 'Mwangaza Roshanee Agency',
                        phoneNumber: "0110 101 102",
                        location: "Ruiru",
                        status: 5,
                        insuranceCompany: "Jubilee Insurance",
                        policyType: "Medical Insurance",
                        policyNo: "001",
                        policyValue: "4000000",
                        commisionValue: "400000",
                        invoiceNo: "002"
                    },
                    {
                        name: 'Mwangaza Roshanee Agency',
                        phoneNumber: "0110 101 102",
                        location: "Ruiru",
                        status: 5,
                        insuranceCompany: "Jubilee Insurance",
                        policyType: "Medical Insurance",
                        policyNo: "001",
                        policyValue: "4000000",
                        commisionValue: "400000",
                        invoiceNo: "002"
                    },
                    {
                        name: 'Mwangaza Roshanee Agency',
                        phoneNumber: "0110 101 102",
                        location: "Ruiru",
                        status: 5,
                        insuranceCompany: "Jubilee Insurance",
                        policyType: "Medical Insurance",
                        policyNo: "001",
                        policyValue: "4000000",
                        commisionValue: "400000",
                        invoiceNo: "002"
                    }
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
        },
        paid() {
            if (this.claims.details.length > 0) {
                return this.claims.details.filter(claim => claim.status === 5)
            }
        }
    },
    methods: {
        getClaimStatus(status) {

            if (status === 0) return 'orange'
            else if (status === 1) return 'green'
            else if (status === 2) return 'red'
            else if (status === 3) return 'blue'
            else if (status === 4) return 'black'
            else return '#3750EB'
        },
        editPolicy(item) {
            this.editedFirmIndex = this.claims.details.indexOf(item)
            this.editedClaims = Object.assign({}, item)
            this.dialogEditClaim = true
        },
    },
}
</script>