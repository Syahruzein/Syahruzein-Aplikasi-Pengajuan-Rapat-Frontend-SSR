<template>
    <div>
        <v-card
        v-if="showAdmin"
        class=" pa-6 mt-4"
        outlined
        tile
        >
            <v-card elevation="3" class="pa-8">
                <v-card-title>
                    Data Akun APR
                    <v-spacer></v-spacer>
                    <v-text-field
                        v-model="search"
                        append-icon="mdi-magnify"
                        label="Search"
                        single-line
                        hide-details
                    ></v-text-field>
                </v-card-title>
                <v-data-table
                    :headers="headers"
                    :items="akun"
                    :search="search"
                    sort-by="id"
                    class="elevation-1"
                ></v-data-table>
            </v-card>
        </v-card>
        <v-card v-if="!showAdmin" class="pa-6 mt-4" outlined tile>
            <v-card elevation="3" class="pa-8">
                <v-alert
                type="error"
                prominent
                border="left"
                >          
                <h2>Required role admin !!!.</h2>
                </v-alert>
            </v-card>
        </v-card>
    </div>
</template>
<script>
export default {
    data() {
        return {
            search: "",
            headers: [
                // { text: "ID", value: "id" },
                { text: "Username", value: "username" },
                { text: "Email", value: "email" },
                { text: "Position", value: "position" },
            ],
            akun: [
                {
                    // "id": 1,
                    "username": "",
                    "email": "",
                    "position": "",
                },
            ],
        }
    },
    methods: {
        async getAuthAll() {
            const getData = await this.$axios(`http://localhost:9200/api/auth/user`);
            this.akun = getData.data;
        },
    },
    computed: {
        currentUser() {
            return this.$store.state.authentication.user;
        },
        showAdmin() {
            if (this.currentUser && this.currentUser.roles) {
            return this.currentUser.roles.includes('ROLE_ADMIN');
            }

            return false;
        },
    },
    mounted() {
        this.getAuthAll();
        if (!this.currentUser) {
            this.$router.push('/');
        }
    },
}
</script>
<style>
    
</style>