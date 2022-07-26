<template>
    <div>
        <v-container fluid class="pa-0 bg-teal">
            <v-row no-gutters>
                <v-col cols="12">
                    <ccamenu />
                </v-col>
            </v-row>

            <v-row no-gutters class="pa-5">

                <v-col class="d-flex justify-end flex-wrap">
                    <v-chip class="ma-2" :color="insuranceTabs ? 'primary' : 'white'" pill @click="toggleTabs(1)">
                        Insurance Agents/ Brokerage /Firms Users
                        <v-icon right>
                            mdi-account-outline
                        </v-icon>
                    </v-chip>
                    <v-chip class="ma-2" :color="adminTabs ? 'primary' : 'white'" pill @click="toggleTabs(2)">
                        Admin User Accounts
                        <v-icon right>
                            mdi-account-outline
                        </v-icon>
                    </v-chip>
                </v-col>

                <v-col cols="12" v-if="insuranceTabs">
                    <v-card class="my-5 pa-4 d-flex justify-end ">
                        <v-dialog v-model="dialog" fullscreen hide-overlay transition="dialog-bottom-transition">
                            <template v-slot:activator="{ on, attrs }">
                                <v-btn color="primary" v-bind="attrs" v-on="on" class="pa-5">
                                    <v-icon left>
                                        {{ icons.mdiAccountMultiplePlus }}
                                    </v-icon>
                                    Add External Users
                                </v-btn>
                            </template>
                            <v-card>
                                <v-toolbar dark color="primary">
                                    <v-btn icon dark @click="closeDialog1">
                                        <v-icon>mdi-close</v-icon>
                                    </v-btn>
                                    <v-toolbar-title>Add Insurance Agents/ Brokerage /Firms Users</v-toolbar-title>
                                </v-toolbar>
                                <v-stepper v-model="e1">
                                    <v-stepper-header>
                                        <v-stepper-step :complete="e1 > 1" step="1">
                                            Contact Details
                                        </v-stepper-step>
                                        <v-divider></v-divider>
                                        <v-stepper-step :complete="e1 > 2" step="2">
                                            Business Details
                                        </v-stepper-step>
                                        <v-divider></v-divider>
                                        <v-stepper-step :complete="e1 > 3" step="3">
                                            Confirmation
                                        </v-stepper-step>


                                    </v-stepper-header>

                                    <v-stepper-items>
                                        <v-stepper-content step="1">

                                            <v-radio-group v-model="radios">
                                                <template v-slot:label>
                                                    <div>
                                                        <p class="font-weight-bold h6">Are you adding an ?</p>
                                                    </div>
                                                </template>
                                                <v-radio value="Insurance Brokerage Firm">
                                                    <template v-slot:label>
                                                        <div><strong class="font-weight-bold h6">Insurance Brokerage
                                                                Firm</strong></div>
                                                    </template>
                                                </v-radio>
                                                <v-radio value="Insurance Agent">
                                                    <template v-slot:label>
                                                        <div><strong class="font-weight-bold h6">Insurance
                                                                Agent</strong></div>
                                                    </template>
                                                </v-radio>
                                                <v-radio value="Insurance Rep Name">
                                                    <template v-slot:label>
                                                        <div><strong class="font-weight-bold h6">Insurance Sales
                                                                Representative</strong></div>
                                                    </template>
                                                </v-radio>
                                            </v-radio-group>

                                            <v-text-field label="What's your Brokerage/Agent/Insurance Rep Name?" filled
                                                required></v-text-field>
                                            <v-text-field label="What's your phone number?" required filled>
                                            </v-text-field>
                                            <v-text-field v-model="email" label="What's your email?" required filled>
                                            </v-text-field>

                                            <v-btn color="primary" @click="e1 = 2">
                                                Continue
                                            </v-btn>

                                            <v-btn text>
                                                Cancel
                                            </v-btn>
                                        </v-stepper-content>

                                        <v-stepper-content step="2">
                                            <v-text-field label="What's your business location?" filled required>
                                            </v-text-field>
                                            <v-text-field
                                                label="What's your IRA license no (if agent or brokerage firm)?"
                                                required filled>
                                            </v-text-field>
                                            <v-text-field
                                                label="What's your business registration no (if agent or brokerage firm) / id no (if sales rep) ?"
                                                required filled></v-text-field>
                                            <v-file-input filled accept="image/*"
                                                label="Upload your business registration no (if agent or brokerage firm) / id no (if sales rep)">
                                            </v-file-input>

                                            <v-checkbox v-model="checkbox">
                                                <template v-slot:label>
                                                    <div>
                                                        I agree to the
                                                        <v-tooltip bottom>
                                                            <template v-slot:activator="{ on }">
                                                                <a target="_blank" href="https://vuetifyjs.com"
                                                                    @click.stop v-on="on">
                                                                    terms and conditions
                                                                </a>
                                                            </template>

                                                        </v-tooltip>

                                                    </div>
                                                </template>
                                            </v-checkbox>


                                            <v-btn color="primary" @click="e1 = 3">
                                                Submit
                                            </v-btn>

                                            <v-btn text @click="e1 = 1">
                                                Go Back
                                            </v-btn>
                                        </v-stepper-content>

                                        <v-stepper-content step="3">

                                            <h1 class="text-center color-blue">Voila !! You are done <v-icon
                                                    aria-label="check all" role="img" aria-hidden="false"
                                                    color="#3750EB" size="32">
                                                    {{ icons.mdiCheckAll }}
                                                </v-icon>
                                            </h1>
                                            <p class="text-center">The user will receive the login link and password on
                                                their email</p>
                                        </v-stepper-content>
                                    </v-stepper-items>
                                </v-stepper>

                            </v-card>
                        </v-dialog>
                        <v-dialog v-model="dialogEdit" hide-overlay transition="dialog-bottom-transition" width="700">

                            <v-card>
                                <v-toolbar dark color="primary">
                                    <v-btn icon dark @click="dialogEdit = false">
                                        <v-icon>mdi-close</v-icon>
                                    </v-btn>
                                    <v-toolbar-title>User Details</v-toolbar-title>
                                </v-toolbar>
                                <v-card-text>
                                    <v-container>
                                        <v-row>
                                            <v-col cols="12">
                                                <table>
                                                    <tr>
                                                        <td class="px-5">Name :</td>
                                                        <td class="px-5">{{ editedSystemUser.name }}</td>
                                                    </tr>
                                                    <tr>
                                                        <td class="px-5">Phone Number:</td>
                                                        <td class="px-5">{{ editedSystemUser.phoneNumber }}</td>
                                                    </tr>
                                                    <tr>
                                                        <td class="px-5">Email:</td>
                                                        <td class="px-5">{{ editedSystemUser.email }}</td>
                                                    </tr>
                                                    <tr>
                                                        <td class="px-5">Location:</td>
                                                        <td class="px-5">{{ editedSystemUser.location }}</td>

                                                    </tr>
                                                    <tr>
                                                        <td class="px-5">IRA License No :</td>
                                                        <td class="px-5">{{ editedSystemUser.iraNo }}</td>
                                                    </tr>
                                                    <tr>
                                                        <td class="px-5">Business Registration Number:</td>
                                                        <td class="px-5">{{ editedSystemUser.regNo }}</td>
                                                    </tr>
                                                    <tr>
                                                        <td class="px-5">Status:</td>
                                                        <td class="px-5 text--orange"
                                                            v-if="editedSystemUser.status === 0">
                                                            <p class="text--orange ma-0">Pending Approval</p>
                                                        </td>
                                                        <td class="px-5 text--green"
                                                            v-else-if="editedSystemUser.status === 1">
                                                            Approved
                                                        </td>
                                                    </tr>


                                                </table>

                                            </v-col>

                                        </v-row>
                                        <v-row>
                                            <v-col v-if="editedSystemUser.status === 0">
                                                <v-btn tile color="primary">
                                                    <v-icon left>
                                                        {{ icons.mdiAccountCheck }}
                                                    </v-icon>
                                                    Approve User
                                                </v-btn>
                                            </v-col>
                                            <v-col>
                                                <v-btn tile color="error">
                                                    <v-icon left>
                                                        {{ icons.mdiAccountCancel }}
                                                    </v-icon>
                                                    Disapprove User
                                                </v-btn>
                                            </v-col>
                                        </v-row>
                                    </v-container>
                                </v-card-text>

                            </v-card>

                        </v-dialog>
                    </v-card>
                    <v-card>
                        <v-tabs fixed-tabs background-color="#3750EB" show-arrows dark v-model="tabs">
                            <v-tab href="#tab-1">All</v-tab>
                            <v-tab href="#tab-2">Approved</v-tab>
                            <v-tab href="#tab-3">Disapproved</v-tab>
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
                                        <v-data-table :headers="headers" :items="users" :search="search"
                                            :items-per-page="10" class="elevation-1">
                                            <template v-slot:item.status="{ item }">
                                                <v-chip :color="getUserStatus(item.status)" dark>
                                                    {{ item.status === 1 ? "Approved" : "Pending Approval" }}
                                                </v-chip>
                                            </template>
                                            <template v-slot:item.actions="{ item }">
                                                <v-icon small class="mr-2" @click="editSytemUser(item)">
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
                                        <v-data-table :headers="headers" :items="approvedUser" :items-per-page="10"
                                            class="elevation-1">
                                            <template v-slot:item.status="{ item }">
                                                <v-chip :color="getUserStatus(item.status)" dark>
                                                    {{ item.status === 1 ? "Approved" : "Pending Approval" }}
                                                </v-chip>
                                            </template>
                                            <template v-slot:item.actions="{ item }">
                                                <v-icon small class="mr-2" @click="editSytemUser(item)">
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
                                        <v-data-table :headers="headers" :items="disapprovedUser" :items-per-page="10"
                                            class="elevation-1">
                                            <template v-slot:item.status="{ item }">
                                                <v-chip :color="getUserStatus(item.status)" dark>
                                                    {{ item.status === 1 ? "Approved" : "Pending Approval" }}
                                                </v-chip>
                                            </template>
                                            <template v-slot:item.actions="{ item }">
                                                <v-icon small class="mr-2" @click="editSytemUser(item)">
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
                <v-col cols="12" v-else>
                    <v-card class="my-5 pa-4 d-flex justify-end ">
                        <v-dialog v-model="dialog2" hide-overlay transition="dialog-bottom-transition" width="700">
                            <template v-slot:activator="{ on, attrs }">
                                <v-btn color="primary" v-bind="attrs" v-on="on" class="pa-5">
                                    <v-icon left>
                                        {{ icons.mdiAccountMultiplePlus }}
                                    </v-icon>
                                    Add Admin Users
                                </v-btn>
                            </template>
                            <v-card>
                                <v-toolbar dark color="primary">
                                    <v-btn icon dark @click="dialog2 = false">
                                        <v-icon>mdi-close</v-icon>
                                    </v-btn>
                                    <v-toolbar-title>Add Admin User</v-toolbar-title>
                                </v-toolbar>
                                <v-card-text>
                                    <v-container>
                                        <v-row>
                                            <v-col cols="12">
                                                <v-text-field v-model="admin.name" label="User Name" filled>
                                                </v-text-field>

                                            </v-col>
                                            <v-col cols="12">
                                                <v-text-field v-model="admin.email" label="User Email" filled>
                                                </v-text-field>
                                            </v-col>

                                            <v-col cols="12">
                                                <v-select :items="admin.roles" filled label="Role"></v-select>
                                            </v-col>


                                            <v-btn color="primary" rounded block>
                                                Add
                                            </v-btn>
                                        </v-row>
                                    </v-container>
                                </v-card-text>

                            </v-card>

                        </v-dialog>


                    </v-card>
                    <v-card>
                        <v-data-table :headers="admin.headers" :items="admin.users" :search="search"
                            :items-per-page="10" class="elevation-1">
                            <template v-slot:item.actions="{ item }">
                                <v-icon small class="mr-2" @click="editAdminUser(item)">
                                    {{ icons.mdiDotsVertical }}
                                </v-icon>

                            </template>

                            <v-dialog v-model="dialogAdmin" hide-overlay transition="dialog-bottom-transition"
                                width="700">

                                <v-card>
                                    <v-toolbar dark color="primary">
                                        <v-btn icon dark @click="dialogAdmin = false">
                                            <v-icon>mdi-close</v-icon>
                                        </v-btn>
                                        <v-toolbar-title>Admin Users Details</v-toolbar-title>
                                    </v-toolbar>
                                    <v-card-text>
                                        <v-container>
                                            <v-row>
                                                <v-col cols="12">
                                                    <table>
                                                        <tr>
                                                            <td class="px-5">Name :</td>
                                                            <td class="px-5">{{ editedAdminUser.name }}</td>
                                                        </tr>
                                                        <tr>
                                                            <td class="px-5">Phone Number:</td>
                                                            <td class="px-5">{{ editedAdminUser.phoneNumber }}</td>
                                                        </tr>
                                                        <tr>
                                                            <td class="px-5">Email:</td>
                                                            <td class="px-5">{{ editedAdminUser.email }}</td>
                                                        </tr>

                                                    </table>

                                                </v-col>

                                            </v-row>
                                            <v-row>
                                                <v-col v-if="editedSystemUser.status === 0">
                                                    <v-btn tile color="primary">
                                                        <v-icon left>
                                                            {{ icons.mdiAccountCheck }}
                                                        </v-icon>
                                                        Approve User
                                                    </v-btn>
                                                </v-col>
                                                <v-col>
                                                    <v-btn tile color="error">
                                                        <v-icon left>
                                                            {{ icons.mdiAccountCancel }}
                                                        </v-icon>
                                                        Disapprove User
                                                    </v-btn>
                                                </v-col>
                                            </v-row>
                                        </v-container>
                                    </v-card-text>

                                </v-card>

                            </v-dialog>

                        </v-data-table>
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
<script scoped>
import { mdiAccountMultiplePlus, mdiDotsVertical, mdiAccountCheck, mdiAccountCancel, mdiPencil, mdiMicrosoftExcel } from "@mdi/js";
export default {
    name: "CcaUsersPage",
    data() {
        return {
            e1: 1,
            search: '',
            email: "",
            adminTabs: false,
            insuranceTabs: true,
            show1: false,
            checkbox: false,
            password: '',
            menuValue: null,
            rules: {
                required: value => !!value || 'Required.',
                min: v => v.length >= 8 || 'Min 8 characters',
                emailMatch: () => (`The email and password you entered don't match`),
            },
            admin: {
                email: '',
                name: '',
                roles: ["Approver", "Payer", "Super Admin"],
                headers: [
                    {
                        text: 'Name',
                        align: 'start',
                        sortable: false,
                        value: 'name',
                    },
                    { text: 'Email', value: 'email' },
                    { text: 'Role', value: 'role' },
                    { text: 'Actions', value: 'actions' },
                ],
                users: [
                    {
                        name: 'Samuel Kariuki',
                        email: "inboxsamuel@outlook.com",
                        role: 'Approver',
                    },
                    {
                        name: 'Felix Fleet',
                        email: "inboxsamuel@outlook.com",
                        role: 'Payer',
                    },
                    {
                        name: 'Samuel Fleet',
                        email: "inboxsamuel@outlook.com",
                        role: 'Super Admin',
                    },
                ]
            },
            dialog: false,
            dialog2: false,
            notifications: false,
            sound: true,
            widgets: false,
            icons: { mdiAccountMultiplePlus, mdiDotsVertical, mdiAccountCheck, mdiAccountCancel, mdiPencil, mdiMicrosoftExcel },
            tabs: null,
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
                { text: 'Role', value: 'role' },
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
                    role: 'Insurance Agency',
                    status: 0
                },
                {
                    name: 'Mwangaza Roshanee Agency',
                    phoneNumber: "0708091524",
                    email: "inboxsamuel@outlook.com",
                    location: "Mombasa Road",
                    iraNo: "01565454",
                    regNo: '01565454',
                    role: 'Insurance Firm',
                    status: 1
                },



            ],
            dialogEdit: false,
            dialogAdmin: false,
            editedSystemUser: {
                name: '',
                phoneNumber: "",
                email: "",
                location: "",
                iraNo: "",
                regNo: '',
                status: false
            },
            editedAdminUser: {
                name: '',
                phoneNumber: "",
                email: "",
            },

        }
    },
    computed: {
        approvedUser() {
            return this.users.filter(user => user.status === 1)
        },
        disapprovedUser() {
            return this.users.filter(user => user.status === 0)
        }
    },
    methods: {
        toggleTabs(tab) {
            if (tab == 1) {
                this.adminTabs = false;
                this.insuranceTabs = true;
            } else {
                this.insuranceTabs = false;
                this.adminTabs = true;

            }
        },
        closeDialog1() {
            this.e1 = 1;
            this.dialog = false
        },
        getUserStatus(status) {
            if (status === 0) return 'red'
            else return 'green'
        },
        editSytemUser(item) {
            this.editedSystemUser = Object.assign({}, item)
            this.dialogEdit = true
        },
        editAdminUser(item) {
            this.editedAdminUser = Object.assign({}, item)
            this.dialogAdmin = true
        },
    },
}
</script>