<template>
    <div>
        <v-card
            v-if="showStaff"
            class=" pa-6 mt-4"
            outlined
            tile
            >
            <v-card elevation="3" class="pa-8">
                <v-card-title>
                    {{ totalMeet }} Rapat Selesai
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
                    :items="meet"
                    :items-per-page="5"
                    :search="search"
                    sort-by="waktu"
                    class="elevation-1"
                >
                    <template v-slot:[getItemTanggal()]="{ item }">
                        <span>{{ new Date(item.tanggal).toLocaleDateString('da') }}</span>
                        <!-- da-DK -->
                    </template>
                    
                    <template v-slot:top>
                            
                            <v-dialog
                            v-model="dialog"
                            scrollable
                            persistent
                            max-width="70rem"
                            transition="dialog-bottom-transition"
                            >
                            <v-card
                            max-width="20rem"
                            height="60vh"
                            >
                                <v-toolbar
                                color="primary"
                                dark
                                ><h2>Detail notulen</h2></v-toolbar>
                                
                            </v-card>
                                <v-card
                                height="60vh"
                                >

                                    <v-card-text
                                    class="pl-6 pt-4"
                                    >
                                        <!-- <div>Word of the Day</div> -->
                                        <p class="text-h4 text--primary">
                                            Ringkasan
                                        </p>
                                        <p>dari Sekretaris</p>
                                        <div v-if="catatans[0].notulen === null" class="text--primary" >
                                            <i class="red--text">Mohon ma'af notulen belum dibuat</i>
                                        </div>
                                        <div v-else class="text--primary " >
                                            {{ catatans[0].notulen }}
                                        </div>
                                    </v-card-text>
                                                                            
                                    <v-expand-transition>
                                        <v-card
                                            v-if="reveal"
                                            class="overflow-y-auto transition-fast-in-fast-out v-card--reveal"
                                            max-width="50rem"
                                            c
                                        >
                                            <v-card-text>
                                                <v-container>
                                                    <v-list
                                                        two-line
                                                        subheader
                                                    >
                                                        <v-subheader class="pt-4 mb-2">
                                                            <p>
                                                                <b class="subheader">{{ selectedItemIndex.maker }} </b> 
                                                                <br> 
                                                                kepada {{ selectedItemIndex.receiver }}
                                                            </p>
                                                        </v-subheader>
                                                        <v-list-item class="mt-2">
                                                        <v-list-item-content>
                                                            <v-list-item-title>
                                                                Yth Bapak/Ibu Undangan 
                                                                <br>Semoga selalu diberikan kesehatan, Aamiin.
                                                            </v-list-item-title>
                                                        </v-list-item-content>
                                                        </v-list-item>
                                                        <v-list-item>
                                                        <v-list-item-content>
                                                            <v-list-item-title>Mohon kehadirannya dalam <b>{{ selectedItemIndex.perihal }} </b> pada :</v-list-item-title>
                                                        </v-list-item-content>
                                                        </v-list-item>
                                                        <v-list-item>
                                                            <v-list-item-content>
                                                                <v-list-item-title>Hari : {{ computedDayDateFormattedMomentjs }}</v-list-item-title>
                                                                <v-list-item-title class="mt-2">Tanggal : {{ computedDateFormattedMomentjs }}</v-list-item-title>
                                                                <v-list-item-title class="mt-2">Jam : {{ selectedItemIndex.waktu }} WIB - Selesai</v-list-item-title>
                                                                <v-list-item-title class="mt-2">Tempat : {{ selectedItemIndex.tempat }}</v-list-item-title>
                                                                <v-list-item-title class="mt-2">Agenda : </v-list-item-title>
                                                                <v-textarea
                                                                readonly
                                                                v-model="selectedItemIndex.deskripsi"
                                                                ></v-textarea>
                                                                <v-list-item-title class="mt-4">Kami mohon hadir tepat waktu. Terima Kasih.</v-list-item-title>
                                                            </v-list-item-content>
                                                        </v-list-item>       
                                                        <v-list-item>
                                                        <v-list-item-content>
                                                            <v-list-item-title class="mt-4">{{ selectedItemIndex.receiver }}</v-list-item-title>
                                                            <v-list-item-title class="mt-4"><b><i class="green--text">Terverifikasi</i></b></v-list-item-title>
                                                            <v-list-item-title class="mt-4">{{ nameVerified[0].username }}</v-list-item-title>
                                                        </v-list-item-content>
                                                        </v-list-item>
                                                        <v-list-item>
                                                        <v-list-item-content>
                                                        </v-list-item-content>
                                                        </v-list-item>
                                                    </v-list>
                                                </v-container>
                                            </v-card-text>
                                            
                                        </v-card>
                                </v-expand-transition>      

                                <v-footer class="pa-2">
                                    <v-spacer></v-spacer>
                                    <v-card-actions 
                                    v-if="reveal === true"
                                    class="pt-0">
                                        <v-btn
                                        class="white--text"
                                        color="bg-gradient-secondary"
                                        @click="reveal = false"
                                        >
                                            Close
                                        </v-btn>
                                    </v-card-actions>
                                    <v-card-actions
                                    v-else
                                    >                                                                                        
                                            <v-btn
                                            class="white--text"
                                            color="bg-gradient-secondary"
                                            @click="close"
                                            >
                                            close
                                            </v-btn>
                                            <v-btn
                                                class="white--text"
                                                color="bg-gradient-warning"
                                                @click="reveal = true"
                                            >
                                                Detail Rapat
                                            </v-btn>
                                            <v-btn
                                            v-if="catatans[0].notulen === null"
                                            class="white--text"
                                            color="bg-gradient-info" 
                                            @click="dialog2 = true"
                                            >
                                                Buat Notulen
                                            </v-btn>
                                            <v-btn
                                            v-else
                                            class="white--text"
                                            color="bg-gradient-info" 
                                            @click="dialog2 = true"
                                            >
                                                update Notulen
                                            </v-btn>
                                    </v-card-actions>
                                </v-footer>
                                    
                                </v-card>
                            </v-dialog>    

                            <v-dialog
                                scrollable
                                persistent
                                v-model="dialog2"
                                max-width="40rem"
                                height="60vh"
                            >
                                <v-card>
                                    <v-toolbar
                                    color="primary"
                                    dark
                                    >
                                        <v-card-title>
                                            <h2>Form notulen rapat</h2>
                                        </v-card-title>
                                    </v-toolbar>                                    
                                    <v-card class="pa-8">
                                        <v-form ref="form" v-model="valid"  lazy-validation>
                                            <v-textarea
                                            outlined
                                            name="input-7-4"
                                            v-model="notulen"
                                            label="Notulen"
                                            :rules="notulenRules"
                                            required
                                            height="20rem"
                                            ></v-textarea>

                                            <v-checkbox
                                            v-model="checkbox"
                                            :rules="checkboxRules"
                                            class="mt-1 mb-2"
                                            label="Do you agree?"
                                            required
                                            ></v-checkbox>

                                            <v-spacer></v-spacer>
                                            <v-btn
                                                color="bg-gradient-secondary"
                                                class="white--text"
                                                @click="clear"
                                            >
                                                Cancel
                                            </v-btn>
                                            <v-btn
                                                :disabled="!valid"
                                                color="bg-gradient-info"
                                                class="white--text"
                                                @click="validate"
                                            >
                                                Save
                                            </v-btn>
                                        </v-form>
                                    </v-card>
                                </v-card>
                            </v-dialog>

                            <v-dialog
                            v-model="dialogUpdate"
                            max-width="50rem"
                            transition="dialog-bottom-transition"
                            persistent
                            >
                                <v-card>
                                    <v-toolbar
                                    color="primary"
                                    dark
                                    >
                                    <h2 v-if="success">Notulen rapat berhasil disimpan</h2>
                                    <h2 v-if="!success">Notulen rapat gagal disimpan</h2>
                                    </v-toolbar>
                                    <v-card-text>
                                    <div class="text pa-12">
                                        <h2 v-if="success">Anda bisa memeriksa di Notulen Rapat, klik dibawah ini :</h2>
                                        <h2 v-if="!success">Anda bisa mencoba Membuat lagi, klik dibawah ini :</h2>
                                        </div>
                                    </v-card-text>
                                    <v-card-actions v-if="!success" class="justify-end">
                                    <v-btn
                                        class="white--text"
                                        color="bg-gradient-info"
                                        @click="closeDialog"
                                    >Close</v-btn>
                                    </v-card-actions>
                                    <v-card-actions v-if="success" class="justify-end">
                                    <v-btn
                                        class="white--text"
                                        color="bg-gradient-info"
                                        @click="closeDialog"
                                        :redirect="`/user/staff/Notulen`"
                                    >Ok</v-btn>
                                    </v-card-actions>
                                </v-card>
                            </v-dialog>
        
                        </template>
                        <template v-slot:[getItemStatus()]="{ item }">
                            <v-chip
                                :color="getColor(item.status)"
                                dark
                            >
                                {{ item.status == 3 ? 'finished' : 'rejected' }}
                            </v-chip>
                        </template>

                    <template v-slot:[getItemActions()]="{ item }">
                            <div>
                                <v-btn
                                small
                                rounded
                                elevation="1"
                                color="bg-gradient-info"
                                class="white--text"
                                @click="editItem(item)"
                                >
                                    DETAIL
                                </v-btn>
                                </div>
                        </template>
                </v-data-table>
            </v-card>
        </v-card>
        <v-card v-if="!showStaff" class="pa-6 mt-4" outlined tile>
            <v-card elevation="3" class="pa-8">
              <v-alert
                type="error"
                prominent
                border="left"
              >          
                <h2>Required role staff !!!.</h2>
              </v-alert>
            </v-card>
        </v-card>
    </div>
</template>
<script>
    import moment from 'moment'
    import 'moment/locale/id'

export default {
    components: {
    },
    data() {
        return {
            search: "",
            editedIndex: -1,
            selectedItemIndex: -1,
            dialog: false,
            dialog2: false,
            dialogUpdate: false,
            isEditing: null,
            menu: false,
            menu2: false,
            reveal: false,
            isOperationsSuccess: false,
            valid: false,
            checkbox: false,
            totalMeet: 0,
            notulen: "",
            headers: [
                    // { text: "ID", value: "id" },
                    // { text: "Perihal", value: "perihal" },
                    { text: "Tanggal", value: "tanggal" },
                    { text: "Waktu", value: "waktu" },
                    { text: "Tempat", value: "tempat" },
                    { text: "Status", value: "status" },
                    // { text: "Deskripsi", value: "deskripsi" },
                    { text: "Actions", value: "actions" },
                ],
                // Pengajuan data rapat
                meet: [
                    {
                        "id": 1,
                        "perihal": "Rapat Senat",
                        "tempat": "H02",
                        "tanggal": "12-08-2022",
                        "waktu": "12:00",
                        "Status": "process",
                        "deskripsi": "Rapat pembahasan peserta didik bcldsmvlkdmvlkdfmvlkfmvlkmfdlvkmfdlkvmdflkvmlkmvklf cdcvidsjvoiwrjfpowefjpowefjpowejfpowejfpowejfpoewjfpowejfpowejfpowejfpowejfpoewjfpoef",
                    },
                ],
                catatans: [{
                    "notulen": "kjasfcjdvjds",
                    "meet_id": "2",
                }],
                nameVerified : [{"username": ""}],
                notulenRules : [
                    v => !!v || 'Notulen is required',
                    v => (v && v.length <= 250) || 'Notulen must be less than 250 characters',
                    v => (v && v.length >= 4) || 'Notulen must be more than 4 characters',
                ],
                checkboxRules : [
                    $v => !!$v || 'You must agree to continue!'
                ],
                defaultItem : {
                    perihal: '',
                    tempat: '',
                    tanggal: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
                    waktu: '',
                    status: '',
                    deskripsi: '',
                },
        }
    },
    methods: {
        async countMeet() {
                const getCount = await this.$axios("http://localhost:9200/meet/count-meet-finish");
                this.totalMeet = getCount.data.total;
                // console.log("data", getData);
            },
        async getMeet() {
            const getData = await this.$axios(`http://localhost:9200/meet/finish`);
            // // if(getData.data.id == userId) {
                this.meet = getData.data;
            // }
            // console.log("data", getData)
        },
        async getNotulen() {
            const meet_id = this.selectedItemIndex.id;
            const getDataNotulen = await this.$axios(`http://localhost:9200/notulen/${meet_id}`)
            // method: 'put',
            this.catatans = getDataNotulen.data;
            // console.log("data", getData)

        },
        async getAuthNameVerified() {
                const position = this.selectedItemIndex.receiver;
                const getData = await this.$axios(`http://localhost:9200/api/auth/user-by-position/${position}`)
                this.nameVerified = getData.data;
            },
        async validate(){
            this.$refs.form.validate()
            if(this.$refs.form.validate()){
                const meet_id = this.selectedItemIndex.id;
                // const data = {notulen: this.notulen, meet_id}
                // console.log(data)

                await this.$axios({
                    method: 'put',
                    url: `http://localhost:9200/notulen/update`,
                    data : {
                        notulen: this.notulen,
                        meet_id
                    }
                }).then(response => {
                    this.isOperationsSuccess = true,
                    this.dialogUpdate = true,
                    console.log(response.data)
                }).catch(e => {
                    this.isOperationsSuccess = false
                    this.dialogUpdate = true
                    console.log(e, 'error')
                    console.log(e.response.data.message)
                })
            }
        },
        getItemTanggal() {
            return "item.tanggal";
        },
        getItemActions() {
            return `item.actions`
        },
        editItem(item) {
            this.editedIndex = this.meet.indexOf(item);
            this.selectedItemIndex = Object.assign({}, item);
            this.getNotulen(this.editedIndex);
            this.getAuthNameVerified(this.editedIndex);
            this.dialog = true;
        },
        close () {
            this.dialog = false
            this.$nextTick(() => {
                this.selectedItemIndex = Object.assign({}, this.defaultItem)
            this.editedIndex = -1
            })
        },
        closeDialog (){
            this.dialog = false
            this.dialog2 = false
            this.dialogUpdate = false
        },
        getItemStatus() {
            return "item.status";
        },
        getColor (status) {
            if (status == '3') return 'blue-grey lighten-2'
            else return 'green'
        },
        clear () {
            this.$refs.form.reset()
            this.dialog2 = false
        },
    },
    mounted() {
        this.getMeet();
        // this.getNotulen();
        this.countMeet();
        if (!this.currentUser) {
            this.$router.push('/');
        }
    },
    computed: {
        currentUser() {
            return this.$store.state.authentication.user;
        },
        showStaff(){
            if (this.currentUser && this.currentUser.roles) {
                return this.currentUser.roles.includes('ROLE_STAFF')
            }

            return false;
        },
        success(){
            return  this.isOperationsSuccess;
        },
        computedDateFormattedMomentjs () {
            return this.selectedItemIndex.tanggal ? moment(this.selectedItemIndex.tanggal).format('dddd, MMMM Do YYYY') : ''
        },
        computedDayDateFormattedMomentjs () {
            return this.selectedItemIndex.tanggal ? moment(this.selectedItemIndex.tanggal).format('dddd') : ''
        },
}
}
</script>
 <style >
    .subheader {
            font-size: 1.2em;
        }
    .v-card--reveal {
        bottom: 0;
        opacity: 1 !important;
        position: absolute;
        width: 100%;
        height: 100%;
    }
    .notulens {
        font-size: 1.2em;
    }
    /* .v-textarea {
        height: 20rem;
    } */
</style>