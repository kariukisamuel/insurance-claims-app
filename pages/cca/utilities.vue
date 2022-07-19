<template>
    <div>
        <v-container fluid class="pa-0 bg-teal">
            <v-row no-gutters>
                <v-col cols="12">
                    <ccamenu />
                </v-col>
            </v-row>
            <v-row no-gutters class="pa-10">
                <v-col cols="12">
                    <v-card class="my-5 pa-4 d-flex justify-space-between">
                        <v-dialog v-model="dialogInsurance" hide-overlay transition="dialog-bottom-transition"
                            width="700">
                            <template v-slot:activator="{ on, attrs }">
                                <v-btn color="primary" v-bind="attrs" v-on="on" class="pa-16">
                                    <v-icon left size="43">
                                        {{ icons.mdiOfficeBuilding }}
                                    </v-icon>
                                    Add Supported Insurance Firms
                                </v-btn>
                            </template>
                            <v-card>
                                <v-toolbar dark color="primary">
                                    <v-btn icon dark @click="dialogInsurance = false">
                                        <v-icon>mdi-close</v-icon>
                                    </v-btn>
                                    <v-toolbar-title>Add Insurance Firms</v-toolbar-title>
                                </v-toolbar>
                                <v-card-text>
                                    <v-container>
                                        <v-row>
                                            <v-col cols="12">
                                                <v-text-field v-model="insurance.name" label="Insurance Firm Name"
                                                    filled></v-text-field>
                                            </v-col>
                                            <v-col cols="12">
                                                <v-text-field v-model="insurance.address" label="Insurance Address"
                                                    filled></v-text-field>
                                            </v-col>
                                            <v-col cols="12">
                                                <v-text-field v-model="insurance.phoneNumber"
                                                    label="Insurance Contact Phone Number" filled></v-text-field>
                                            </v-col>
                                            <v-btn color="primary" rounded block>
                                                Save
                                            </v-btn>
                                        </v-row>
                                    </v-container>
                                </v-card-text>


                            </v-card>

                        </v-dialog>

                        <v-dialog v-model="dialogInsuranceType" hide-overlay transition="dialog-bottom-transition"
                            width="700">
                            <template v-slot:activator="{ on, attrs }">
                                <v-btn color="primary" v-bind="attrs" v-on="on" class="pa-16">
                                    <v-icon left size="43">
                                        {{ icons.mdiFormatListBulletedType }}
                                    </v-icon>
                                    Add Supported Insurance Types
                                </v-btn>
                            </template>
                            <v-card>
                                <v-toolbar dark color="primary">
                                    <v-btn icon dark @click="dialogInsurance = false">
                                        <v-icon>mdi-close</v-icon>
                                    </v-btn>
                                    <v-toolbar-title>Add Supported Insurance Types</v-toolbar-title>
                                </v-toolbar>
                                <v-card-text>

                                    <v-container>
                                        <v-row>
                                            <v-col cols="12">
                                                <v-select :items="insuranceFirms" filled label="Select Insurance Firm">
                                                </v-select>
                                            </v-col>
                                            <v-col cols="12">
                                                <v-text-field v-model="insurance.type" label="Type Of Insurance" filled>
                                                </v-text-field>
                                            </v-col>
                                            <v-btn color="primary" rounded block>
                                                Save
                                            </v-btn>
                                        </v-row>
                                    </v-container>
                                </v-card-text>


                            </v-card>

                        </v-dialog>
                        <v-dialog v-model="dialogBank" hide-overlay transition="dialog-bottom-transition" width="700">
                            <template v-slot:activator="{ on, attrs }">
                                <v-btn color="primary" v-bind="attrs" v-on="on" class="pa-16">
                                    <v-icon left size="43">
                                        {{ icons.mdiOfficeBuilding }}
                                    </v-icon>
                                    Add Supported Banks
                                </v-btn>
                            </template>
                            <v-card>
                                <v-toolbar dark color="primary">
                                    <v-btn icon dark @click="dialogBank = false">
                                        <v-icon>mdi-close</v-icon>
                                    </v-btn>
                                    <v-toolbar-title>Add Supported Banks</v-toolbar-title>
                                </v-toolbar>
                                <v-card-text>
                                    <v-container>
                                        <v-row>
                                            <v-col cols="12">
                                                <v-text-field v-model="banks.name" label="Bank Name" filled>
                                                </v-text-field>
                                            </v-col>
                                            <v-col cols="12">
                                                <v-text-field v-model="banks.address" label="Bank Address" filled>
                                                </v-text-field>
                                            </v-col>
                                            <v-col cols="12">
                                                <v-text-field v-model="banks.phoneNumber"
                                                    label="Bank Contact Phone Number" filled></v-text-field>
                                            </v-col>
                                            <v-btn color="primary" rounded block>
                                                Save
                                            </v-btn>
                                        </v-row>
                                    </v-container>
                                </v-card-text>


                            </v-card>

                        </v-dialog>

                        <v-dialog v-model="dialogEditFirm" hide-overlay transition="dialog-bottom-transition"
                            width="700">

                            <v-card>
                                <v-toolbar dark color="primary">
                                    <v-btn icon dark @click="dialog = false">
                                        <v-icon>mdi-close</v-icon>
                                    </v-btn>
                                    <v-toolbar-title>Insurance Firm Details</v-toolbar-title>
                                </v-toolbar>
                                <v-card-text>
                                    <v-container>
                                        <v-row>
                                            <v-col cols="12">
                                                <h2>Name:<span class="font-weight-medium"> {{
                                                        insuranceFirms.firms[0].name
                                                }}</span>
                                                </h2>
                                            </v-col>
                                            <v-col cols="12">
                                                <h2>Phone Number:<span class="font-weight-medium"> {{
                                                        insuranceFirms.firms[0].phoneNumber
                                                }}</span>
                                                </h2>
                                            </v-col>
                                            <v-col cols="12">
                                                <h2>Address:<span class="font-weight-medium"> {{
                                                        insuranceFirms.firms[0].address
                                                }}</span>
                                                </h2>
                                            </v-col>
                                            <v-col cols="12">
                                                <h2>Email:<span class="font-weight-medium"> {{
                                                        insuranceFirms.firms[0].email
                                                }}</span>
                                                </h2>
                                            </v-col>


                                        </v-row>
                                        <v-row>

                                            <v-col cols="4">
                                                <v-btn tile color="error">
                                                    <v-icon left>
                                                        {{ icons.mdiAccountCancel }}
                                                    </v-icon>
                                                    Disapprove Firm
                                                </v-btn>
                                            </v-col>
                                            <v-col cols="4">
                                                <v-btn tile color="success">
                                                    <v-icon left>
                                                        {{ icons.mdiPencil }}
                                                    </v-icon>
                                                    Edit User
                                                </v-btn>
                                            </v-col>

                                        </v-row>
                                    </v-container>
                                </v-card-text>

                            </v-card>

                        </v-dialog>
                    </v-card>

                    <v-card>
                        <v-tabs fixed-tabs background-color="#3750EB" dark v-model="tabs">
                            <v-tab href="#tab-1">Supported Insurance Firms</v-tab>
                            <v-tab href="#tab-2">Supported Insurance Types</v-tab>
                            <v-tab href="#tab-3">Supported Insurance Banks</v-tab>
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
                                        <v-text-field v-model="search" append-icon="mdi-magnify" label="Search"
                                            single-line hide-details></v-text-field>
                                    </v-card-title>
                                    <v-card-text>
                                        <v-data-table :headers="insuranceFirms.headers" :items="insuranceFirms.firms"
                                            :items-per-page="10" class="elevation-1">

                                            <template v-slot:item.actions="{ item }">
                                                <v-icon small class="mr-2" @click="editFirm(item)">
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
                                        <v-text-field v-model="search" append-icon="mdi-magnify" label="Search"
                                            single-line hide-details></v-text-field>
                                    </v-card-title>
                                    <v-card-text>
                                        <v-data-table :headers="insuranceTypes.headers" :items="insuranceTypes.types"
                                            :items-per-page="10" class="elevation-1">
                                            <template v-slot:item.actions="{ item }">
                                                <v-icon small class="mr-2" @click="editItem(item)">
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
                                        <v-text-field v-model="search" append-icon="mdi-magnify" label="Search"
                                            single-line hide-details></v-text-field>
                                    </v-card-title>
                                    <v-card-text>
                                        <v-data-table :headers="supportedBanks.headers" :items="supportedBanks.banks"
                                            :items-per-page="10" class="elevation-1">
                                            <template v-slot:item.actions="{ item }">
                                                <v-icon small class="mr-2" @click="editItem(item)">
                                                    {{ icons.mdiDotsVertical }}
                                                </v-icon>
                                            </template>
                                        </v-data-table>

                                    </v-card-text>
                                </v-card>
                            </v-tab-item>
                        </v-tabs-items>
                    </v-card>
                </v-col>
            </v-row>

        </v-container>
    </div>


</template>
<style>
.bg-teal {
    background-color: rgb(231 240 247);
}

.bg-blue {
    background-color: #3750EB;
}
</style>
<script>
import { mdiAccountMultiplePlus, mdiDotsVertical, mdiAccountCheck, mdiAccountCancel, mdiPencil, mdiOfficeBuilding, mdiFormatListBulletedType, mdiMicrosoftExcel } from "@mdi/js";
export default {
    name: "CcaUsersPage",
    data() {
        return {
            search:'',
            insuranceFirms: ['Jubilee Insurance', 'Icea Insurance', 'Old Mutual', 'Amaco'],
            banks: {
                name: "",
                address: "",
                phoneNumber: ""
            },
            insurance: {
                name: "",
                address: "",
                phoneNumber: ""
            },
            e1: 1,
            email: "",
            show1: false,
            checkbox: false,
            password: '',
            menuValue: null,
            rules: {
                required: value => !!value || 'Required.',
                min: v => v.length >= 8 || 'Min 8 characters',
                emailMatch: () => (`The email and password you entered don't match`),
            },
            dialog: false,
            notifications: false,
            sound: true,
            widgets: false,
            icons: { mdiAccountMultiplePlus, mdiDotsVertical, mdiAccountCheck, mdiAccountCancel, mdiPencil, mdiOfficeBuilding, mdiFormatListBulletedType,mdiMicrosoftExcel },
            tabs: null,
            insuranceFirms: {
                headers: [
                    {
                        text: 'Name',
                        align: 'start',
                        sortable: false,
                        value: 'name',
                    },
                    { text: 'Address', value: 'address' },
                    { text: 'Contact Phone Number', value: 'phoneNumber' },
                    { text: 'Email', value: 'email' },
                    { text: 'Actions', value: 'actions' },
                ],
                firms: [
                    {
                        name: 'Jubilee Insurance',
                        address: "P.O Box 156564, Nairobi",
                        phoneNumber: "0708091524",
                        email: "inboxsamuel@outlook.com"
                    },
                    {
                        name: 'Jubilee Insurance',
                        address: "P.O Box 156564, Nairobi",
                        phoneNumber: "0708091524",
                        email: "inboxsamuel@outlook.com"
                    },
                    {
                        name: 'Jubilee Insurance',
                        address: "P.O Box 156564, Nairobi",
                        phoneNumber: "0708091524",
                        email: "inboxsamuel@outlook.com"
                    },
                    {
                        name: 'Jubilee Insurance',
                        address: "P.O Box 156564, Nairobi",
                        phoneNumber: "0708091524",
                        email: "inboxsamuel@outlook.com"
                    },
                    {
                        name: 'Jubilee Insurance',
                        address: "P.O Box 156564, Nairobi",
                        phoneNumber: "0708091524",
                        email: "inboxsamuel@outlook.com"
                    },
                    {
                        name: 'Jubilee Insurance',
                        address: "P.O Box 156564, Nairobi",
                        phoneNumber: "0708091524",
                        email: "inboxsamuel@outlook.com"
                    },
                    {
                        name: 'Jubilee Insurance',
                        address: "P.O Box 156564, Nairobi",
                        phoneNumber: "0708091524",
                        email: "inboxsamuel@outlook.com"
                    },
                    {
                        name: 'Jubilee Insurance',
                        address: "P.O Box 156564, Nairobi",
                        phoneNumber: "0708091524",
                        email: "inboxsamuel@outlook.com"
                    },
                    {
                        name: 'Jubilee Insurance',
                        address: "P.O Box 156564, Nairobi",
                        phoneNumber: "0708091524",
                        email: "inboxsamuel@outlook.com"
                    },
                    {
                        name: 'Jubilee Insurance',
                        address: "P.O Box 156564, Nairobi",
                        phoneNumber: "0708091524",
                        email: "inboxsamuel@outlook.com"
                    },
                ]
            },
            insuranceTypes: {
                headers: [
                    {
                        text: 'Name',
                        align: 'start',
                        sortable: false,
                        value: 'name',
                    },
                    { text: 'Type Of Insurance', value: 'typeOfInsurance' },
                    { text: 'Actions', value: 'actions' },
                ],
                types: [
                    {
                        name: 'Jubilee Insurance',
                        typeOfInsurance: "Medical Insurance",
                    },
                    {
                        name: 'Jubilee Insurance',
                        typeOfInsurance: "Medical Insurance",
                    },
                    {
                        name: 'Jubilee Insurance',
                        typeOfInsurance: "Medical Insurance",
                    },
                    {
                        name: 'Jubilee Insurance',
                        typeOfInsurance: "Medical Insurance",
                    },
                    {
                        name: 'Jubilee Insurance',
                        typeOfInsurance: "Medical Insurance",
                    },
                    {
                        name: 'Jubilee Insurance',
                        typeOfInsurance: "Medical Insurance",
                    }
                ]
            },
            supportedBanks: {
                headers: [
                    {
                        text: 'Name',
                        align: 'start',
                        sortable: false,
                        value: 'name',
                    },
                    { text: 'Address', value: 'address' },
                    { text: 'Phone Number', value: 'phoneNumber' },
                    { text: 'Actions', value: 'actions' },
                ],
                banks: [
                    {
                        name: 'Diamond Trust Bank',
                        address: "P.O Box 163, Nairobi",
                        phoneNumber: "0110 101 102",
                    },
                    {
                        name: 'Diamond Trust Bank',
                        address: "P.O Box 163, Nairobi",
                        phoneNumber: "0110 101 102",
                    },
                    {
                        name: 'Diamond Trust Bank',
                        address: "P.O Box 163, Nairobi",
                        phoneNumber: "0110 101 102",
                    },
                    {
                        name: 'Diamond Trust Bank',
                        address: "P.O Box 163, Nairobi",
                        phoneNumber: "0110 101 102",
                    },
                    {
                        name: 'Diamond Trust Bank',
                        address: "P.O Box 163, Nairobi",
                        phoneNumber: "0110 101 102",
                    },
                ]
            },

            headers: [
                {
                    text: 'Name',
                    align: 'start',
                    sortable: false,
                    value: 'name',
                },
                { text: 'Phone Number', value: 'phoneNumber' },
                { text: 'Email', value: 'email' },
                { text: 'Location', value: 'location' },
                { text: 'IRA No', value: 'iraNo' },
                { text: 'Business Registration No', value: 'regNo' },
                { text: 'Status', value: 'status' },
                { text: 'Actions', value: 'actions' },
            ],
            users: [
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: true
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: false
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: true
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: false
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: true
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: false
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: true
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: false
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: true
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: false
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: true
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: false
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: true
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: false
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: true
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: false
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: true
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: false
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: true
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: false
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: true
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    status: false
                },


            ],
            dialogInsurance: false,
            dialogInsuranceType: false,
            dialogBank: false,
            editedFirm: {
                name: '',
                address: "",
                phoneNumber: "",
            },
            editedFirmIndex: '',
            dialogEditFirm: ''
        }
    },
    methods: {
        getUserStatus(status) {
            if (status) return 'green'
            else return 'red'
        },
        editFirm(item) {
            this.editedFirmIndex = this.insuranceFirms.firms.indexOf(item)
            this.editedFirm = Object.assign({}, item)
            this.dialogEditFirm = true
        },
    },
}
</script>