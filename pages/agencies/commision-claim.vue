<template>

    <v-container fluid class="pa-0 bg-teal">
        <v-row no-gutters>
            <v-col cols="12">
                <agencymenu />
            </v-col>
        </v-row>
        <v-row no-gutters class="pa-10">
            <v-col cols="12">
                <v-card class="my-5 pa-4 ">
                    <div class="d-flex justify-center ">
                        <h4> By
                            using our platform you dont have to wait for 45-60 days to get your commisions paid.Get paid
                            faster</h4>
                    </div>

                    <div class="d-flex justify-center my-3">
                        <v-dialog v-model="claimDialog" fullscreen hide-overlay transition="dialog-bottom-transition">
                            <template v-slot:activator="{ on, attrs }">
                                <v-btn color="primary" v-bind="attrs" v-on="on">
                                    <v-icon left>
                                        {{ icons.mdiPlusBoxMultipleOutline }}
                                    </v-icon>
                                    Make A New Commission Claim Request
                                </v-btn>
                            </template>
                            <v-card class="bg-teal">
                                <v-toolbar dark color="primary">
                                    <v-btn icon dark @click="claimDialog = false">
                                        <v-icon>mdi-close</v-icon>
                                    </v-btn>
                                    <v-toolbar-title>Submit Policy Details:</v-toolbar-title>
                                </v-toolbar>
                                <v-stepper v-model="e1">
                                    <v-stepper-header>
                                        <v-stepper-step :complete="e1 > 1" step="1">

                                        </v-stepper-step>

                                        <v-divider></v-divider>

                                        <v-stepper-step :complete="e1 > 2" step="2">

                                        </v-stepper-step>

                                        <v-divider></v-divider>

                                        <v-stepper-step step="3">

                                        </v-stepper-step>
                                    </v-stepper-header>


                                    <v-stepper-items>
                                        <v-stepper-content step="1">
                                            <v-card-text>
                                                <v-container>
                                                    <v-row>
                                                        <v-col cols="12">
                                                            <v-select :items="insuranceCompanies" filled
                                                                label="With which insurance firm is the policy being insured in ?">
                                                            </v-select>
                                                        </v-col>
                                                        <v-col cols="12">
                                                            <v-select :items="insuranceCompanies" filled
                                                                label="What type of policy ?">
                                                            </v-select>
                                                        </v-col>
                                                        <v-col cols="12">
                                                            <v-text-field label="What's the policy number ?" filled>
                                                            </v-text-field>
                                                        </v-col>

                                                        <v-col cols="12">
                                                            <v-btn color="primary" @click="e1 = 2">
                                                                Continue
                                                            </v-btn>
                                                        </v-col>
                                                    </v-row>
                                                </v-container>
                                            </v-card-text>
                                        </v-stepper-content>

                                        <v-stepper-content step="2">
                                            <v-card-text>
                                                <v-container>
                                                    <v-row>
                                                        <v-col cols="12">
                                                            <v-file-input truncate-length="15" show-size
                                                                label="Upload a copy of the policy">
                                                            </v-file-input>
                                                        </v-col>
                                                        <v-col cols="12">
                                                            <v-select :items="years" filled
                                                                label="What's the policy period?">
                                                            </v-select>
                                                        </v-col>
                                                        <v-col cols="12">
                                                            <v-text-field label="What's the insurance premium amount ?"
                                                                filled>
                                                            </v-text-field>
                                                        </v-col>
                                                        <v-col cols="12">

                                                            <v-btn color="primary" @click="e1 = 3">
                                                                Continue
                                                            </v-btn>

                                                            <v-btn text @click="e1 = 1" class="ml-3">
                                                                Go Back
                                                            </v-btn>

                                                        </v-col>
                                                    </v-row>
                                                </v-container>
                                            </v-card-text>

                                        </v-stepper-content>

                                        <v-stepper-content step="3">
                                            <v-card-text>
                                                <v-container>
                                                    <v-row>
                                                        <v-col cols="12">
                                                            <v-text-field label="What's your expected commision ?"
                                                                filled>
                                                            </v-text-field>
                                                        </v-col>

                                                        <v-col cols="12">
                                                            <v-text-field label="What's the invoice no ?" filled>
                                                            </v-text-field>
                                                        </v-col>
                                                        <v-col cols="12">
                                                            <v-file-input truncate-length="15" show-size
                                                                label="Upload a copy of the invoice">
                                                            </v-file-input>
                                                        </v-col>
                                                        <v-col cols="12">
                                                            <v-btn color="primary">
                                                                Submit
                                                            </v-btn>
                                                            <v-btn text @click="e1 = 2" class="ml-2">
                                                                Go Back
                                                            </v-btn>
                                                        </v-col>

                                                    </v-row>
                                                </v-container>
                                            </v-card-text>
                                        </v-stepper-content>
                                    </v-stepper-items>
                                </v-stepper>


                            </v-card>
                        </v-dialog>
                    </div>

                </v-card>


                <v-card>
                    <v-tabs fixed-tabs background-color="#3750EB" dark v-model="tabs">
                        <v-tab href="#tab-1">Your Submissions</v-tab>
                        <v-tab href="#tab-2">Disapproved For Payment By Insurance</v-tab>
                        <v-tab href="#tab-3">Approved For Payment By Insurance</v-tab>
                        <v-tab href="#tab-5">Disapproved For Payment By CFA</v-tab>
                        <v-tab href="#tab-4">Approved For Payment By CFA</v-tab>


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
                                <v-row class="py-2">
                                    <v-col cols="12">

                                        <template>
                                            <v-stepper>
                                                <v-stepper-header>
                                                    <v-stepper-step complete step="1">
                                                        Pending Insurance Approval
                                                    </v-stepper-step>

                                                    <v-divider></v-divider>

                                                    <v-stepper-step step="2" >
                                                        Approved By Insurance
                                                    </v-stepper-step>

                                                    <v-divider></v-divider>

                                                    <v-stepper-step step="3">
                                                        Approved For Payment
                                                    </v-stepper-step>
                                                </v-stepper-header>
                                            </v-stepper>
                                        </template>
                                    </v-col>

                                </v-row>
                            </v-container>
                        </v-card-text>
                        <v-card-text>
                            <v-container>
                                <v-row class="py-4">
                                    <v-col cols="12">
                                        <v-expansion-panels>
                                            <v-expansion-panel key="1">
                                                <v-expansion-panel-header>
                                                    Type Of Policy
                                                </v-expansion-panel-header>
                                                <v-expansion-panel-content>
                                                    {{ editedClaims.typeOfPolicy }}
                                                </v-expansion-panel-content>
                                            </v-expansion-panel>
                                            <v-expansion-panel key="2">
                                                <v-expansion-panel-header>
                                                    Insurance Company
                                                </v-expansion-panel-header>
                                                <v-expansion-panel-content>
                                                    {{ editedClaims.insurance }}
                                                </v-expansion-panel-content>
                                            </v-expansion-panel>
                                            <v-expansion-panel key="3">
                                                <v-expansion-panel-header>
                                                    Policy No
                                                </v-expansion-panel-header>
                                                <v-expansion-panel-content>
                                                    {{ editedClaims.policyNo }}
                                                </v-expansion-panel-content>
                                            </v-expansion-panel>
                                            <v-expansion-panel key="7">
                                                <v-expansion-panel-header>
                                                    Policy Uploads
                                                </v-expansion-panel-header>
                                                <v-expansion-panel-content>
                                                    <img src="https://via.placeholder.com/500" />
                                                </v-expansion-panel-content>
                                            </v-expansion-panel>
                                            <v-expansion-panel key="3">
                                                <v-expansion-panel-header>
                                                    Policy Period
                                                </v-expansion-panel-header>
                                                <v-expansion-panel-content>
                                                    {{ editedClaims.policyPeriod }}
                                                </v-expansion-panel-content>
                                            </v-expansion-panel>
                                            <v-expansion-panel key="4">
                                                <v-expansion-panel-header>
                                                    Premiums
                                                </v-expansion-panel-header>
                                                <v-expansion-panel-content>
                                                    {{ editedClaims.premiums }}
                                                </v-expansion-panel-content>
                                            </v-expansion-panel>
                                            <v-expansion-panel key="5">
                                                <v-expansion-panel-header>
                                                    Commision
                                                </v-expansion-panel-header>
                                                <v-expansion-panel-content>
                                                    {{ editedClaims.commision }}
                                                </v-expansion-panel-content>
                                            </v-expansion-panel>
                                            <v-expansion-panel key="5">
                                                <v-expansion-panel-header>
                                                    Invoice No
                                                </v-expansion-panel-header>
                                                <v-expansion-panel-content>
                                                    {{ editedClaims.invoiceNo }}
                                                </v-expansion-panel-content>
                                            </v-expansion-panel>
                                            <v-expansion-panel key="5">
                                                <v-expansion-panel-header>
                                                    Status
                                                </v-expansion-panel-header>
                                                <v-expansion-panel-content>


                                                    <v-chip :color="getClaimStatus(editedClaims.status)" dark
                                                        v-if="editedClaims.status === 0">
                                                        Pending Insurance Approval
                                                    </v-chip>
                                                    <v-chip :color="getClaimStatus(editedClaims.status)" dark
                                                        v-else-if="editedClaims.status === 1">
                                                        Approved By Insurance
                                                    </v-chip>
                                                    <v-chip :color="getClaimStatus(editedClaims.status)" dark
                                                        v-else-if="editedClaims.status === 2">
                                                        Rejected By Insurance
                                                    </v-chip>
                                                    <v-chip :color="getClaimStatus(editedClaims.status)" dark
                                                        v-else-if="editedClaims.status === 3">
                                                        Approved For Payment
                                                    </v-chip>
                                                    <v-chip :color="getClaimStatus(editedClaims.status)" dark
                                                        v-else-if="editedClaims.status === 4">
                                                        Payment Rejected
                                                    </v-chip>



                                                </v-expansion-panel-content>
                                            </v-expansion-panel>


                                            <v-expansion-panel key="6">
                                                <v-expansion-panel-header>
                                                    Invoice Uploads
                                                </v-expansion-panel-header>
                                                <v-expansion-panel-content>
                                                    <img src="https://via.placeholder.com/500" />
                                                </v-expansion-panel-content>
                                            </v-expansion-panel>
                                        </v-expansion-panels>
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
import { mdiDotsVertical, mdiMicrosoftExcel, mdiPlusBoxMultipleOutline } from "@mdi/js";
export default {
    name: 'ClaimsPage',
    data() {
        return {
            e1: 1,
            insuranceCompanies: ['AAR Insurance Kenya Limited',
                'Africa Merchant Assurance Company Limited',
                'AIG Kenya Insurance Company Limited',
                'APA Insurance Limited',
                'APA Life Assurance Limited',
                'Barclays Life Assurance Kenya Limited',
                'Britam General Insurance Company (Kenya) Limited',
                'British-American Insurance Company (K) Limited',
                'Cannon Assurance Limited',
                'Capex Life Assurance Company Limited',
                'CIC General Insurance Limited',
                'CIC Life Assurance Limited',
                'Continental Reinsurance Limited',
                'Corporate Insurance Company Limited',
                'Directline Assurance Company Limited'],
            years: ['1 year', '2 years', '3 years', '4 years', '5 years', '6 years', '7 years', '8 years', '9 years', '10 years'],
            claimDialog: false,
            tabs: null,
            icons: { mdiDotsVertical, mdiMicrosoftExcel, mdiPlusBoxMultipleOutline },
            claims: {
                headers: [
                    {
                        text: 'Type Of Policy',
                        align: 'start',
                        sortable: false,
                        value: 'typeOfPolicy',
                    },
                    { text: 'Insured With', value: 'insurance' },
                    { text: 'Policy No', value: 'policyNo' },
                    { text: 'Policy Period', value: 'policyPeriod' },
                    { text: 'Insurance Premium', value: 'premiums' },
                    { text: 'Expected Commision', value: 'commision' },
                    { text: 'Invoice No', value: 'invoiceNo' },
                    { text: 'Status', value: 'status' },
                    { text: 'Actions', value: 'actions' },


                ],
                details: [
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 0
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 1
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 2
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 3
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 4
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 1
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 0
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 1
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 2
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 3
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 4
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 1
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 0
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 1
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 2
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 3
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 4
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 1
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 0
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 1
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 2
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 3
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 4
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 1
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 0
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 1
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 2
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 3
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 4
                    },
                    {
                        typeOfPolicy: "Medical Insurance",
                        insurance: "Jubilee Insurance",
                        policyNo: "00178",
                        policyPeriod: "1 year",
                        premiums: "4,000,000",
                        commision: "400,000",
                        invoiceNo: "001",
                        status: 1
                    },


                ]
            },
            editedPolicyIndex: '',
            editedClaims: {
                typeOfPolicy: "",
                insurance: "",
                policyNo: "",
                policyPeriod: "",
                premiums: "",
                commision: "",
                invoiceNo: "",
                status: ""
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