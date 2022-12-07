<template>
    <div id="Middleview">
    <v-app>
    <div id="body">
        <v-container>
            <v-row align="stretch">
                <v-col
                cols="12" 
                align="center"
                >
                <br><br><br><br>
                <h5 class="fs-2 fw-bold " data-aos="fade-up" data-aos-duration="1000"> Alur Pengajuan <p class="fs-6 text-muted" data-aos="fade-up" data-aos-duration="1300"> Seperti inilah alur dari proses pengajuan suatu agenda rapat</p></h5>
                <br>
                </v-col>
            </v-row>
            <v-container>
                <v-row>
                    <v-col
                    cols="12"
                    sm="4"
                    >                    
                        <v-card
                        elevation="8"
                        class="pt-10 rounded-xl"
                        outlined
                        data-aos="fade-down-right" data-aos-duration="1500"
                        >
                            <v-row>
                                <v-col
                                align="center"
                                >
                                    <i class="fas fa-2x fa-user-check fas-round bg-gradient-info "></i>
                                </v-col>
                            </v-row>
                            <v-card-title primary-title>
                                    <v-spacer></v-spacer>
                                    <h4 class="fw-bold">Masuk</h4>
                                    <v-spacer></v-spacer>
                            </v-card-title>
                            <v-card-text align="center">
                                <p class="text-muted text-lg">Anda perlu masuk <br> untuk mengajukan <br> rapat Anda</p>
                            </v-card-text>
                        </v-card>
                    </v-col>

                    <v-col
                    cols="12"
                    sm="4"
                    >                    
                        <v-card
                        elevation="8"
                        class="pt-10 rounded-xl"
                        outlined
                        data-aos="zoom-in-down" data-aos-duration="1500"
                        >
                            <v-row>
                                <v-col
                                align="center"
                                >
                                    <i class="fas fa-2x fa-file-alt fas-round bg-gradient-info "></i>
                                </v-col>
                            </v-row>
                            <v-card-title primary-title>
                                    <v-spacer></v-spacer>
                                    <h4 class="fw-bold">Isi Biodata Rapat</h4>
                                    <v-spacer></v-spacer>
                            </v-card-title>
                            <v-card-text align="center">
                                <p class="text-muted text-lg">Anda harus mengisi formulir <br> rencana rapat yang akan <br> di agendakan</p>
                            </v-card-text>
                        </v-card>
                    </v-col>

                    <v-col
                    cols="12"
                    sm="4"
                    >                    
                        <v-card
                        elevation="8"
                        class="pt-10 rounded-xl"
                        outlined
                        data-aos="fade-down-left" data-aos-duration="1500"
                        >
                            <v-row>
                                <v-col
                                align="center"
                                >
                                    <i class="fas fa-2x fa-paper-plane fas-round bg-gradient-info "></i>
                                </v-col>
                            </v-row>
                            <v-card-title primary-title>
                                    <v-spacer></v-spacer>
                                    <h4 class="fw-bold">Ajukan Rapat</h4>
                                    <v-spacer></v-spacer>
                            </v-card-title>
                            <v-card-text align="center">
                                <p class="text-muted text-lg">Kirim hasil pengisian biodata <br> rapat untuk diproses oleh <br> pihak manajemen</p>
                            </v-card-text>
                        </v-card>
                    </v-col>
                </v-row>
                <br>
                <v-row
                class="justify-center"
                >
                    <v-col
                    cols="12"
                    sm="4"
                    >                    
                        <v-card
                        elevation="8"
                        class="pt-10 rounded-xl"
                        outlined
                        data-aos="fade-up-right" data-aos-duration="1500"
                        >
                            <v-row>
                                <v-col
                                align="center"
                                >
                                    <i class="fas fa-2x fa-check-circle fas-round bg-gradient-info "></i>
                                </v-col>
                            </v-row>
                            <v-card-title primary-title>
                                    <v-spacer></v-spacer>
                                    <h4 class="fw-bold">Konfirmasi Rapat</h4>
                                    <v-spacer></v-spacer>
                            </v-card-title>
                            <v-card-text align="center">
                                <p class="text-muted text-lg">Jika status permohonan <br> disetujui maka permohonan <br> rapat diterima</p>
                            </v-card-text>
                        </v-card>
                    </v-col>
                    <v-col
                    cols="12"
                    sm="4"
                    >                    
                        <v-card
                        elevation="8"
                        class="pt-10 rounded-xl"
                        outlined
                        data-aos="fade-up-left" data-aos-duration="1500"
                        >
                            <v-row>
                                <v-col
                                align="center"
                                >
                                    <i class="fas fa-2x fa-calendar-alt fas-round bg-gradient-info "></i>
                                </v-col>
                            </v-row>
                            <v-card-title primary-title>
                                    <v-spacer></v-spacer>
                                    <h4 class="fw-bold">Jadwal Rapat</h4>
                                    <v-spacer></v-spacer>
                            </v-card-title>
                            <v-card-text align="center">
                                <p class="text-muted text-lg">Anda dapat melihat data <br> jadwal rapat yang diajukan <br> atau dibuat</p>
                            </v-card-text>
                        </v-card>
                    </v-col>
                </v-row>
                <br>
                <br>
                <br>
                <v-row
                class="justify-center"
                >
                <v-col
                cols="12"
                >                    
                    <v-card
                    elevation="8"
                    class="pt-14 pb-8 rounded-xl"
                    outlined
                    data-aos="zoom-in-up" data-aos-duration="1500"
                    >
                        <v-row>
                            <v-col
                            align="center"
                            >
                                <i class="fas fa-2x fa-scroll fas-round bg-gradient-info "></i>
                            </v-col>
                        </v-row>
                        <v-card-title primary-title>
                                <v-spacer></v-spacer>
                                <h4 class="fw-bold">Tentang Kami</h4>
                                <v-spacer></v-spacer>
                        </v-card-title>
                        <v-card-text align="center">
                            <p class="text-muted text-lg">“ APR adalah aplikasi pengajuan rapat yang dibangun untuk memenuhi kebutuhan agenda rapat. APR dapat membangun suatu system pengajuan rapat yang dapat memanajemen pengajuan rapat serta menjadwalkan rapat yang tepat, akurat dan sistematis di Politeknik Elektronika Negeri Surabaya. “</p>
                            <br><p class="text-lg">~ 17 Oktober 2021 ~</p>
                        </v-card-text>
                    </v-card>
                </v-col>
                </v-row>
            </v-container>
        </v-container>
    </div>
</v-app>
</div>
</template>
<script>
export default {
    
}
</script>
<style scoped>

.fs-6 {
    padding-top: 0.5rem;
}
i.fas-round {
    display: inline-block;
    width: 4.5rem;
    height: 4.5rem;
    border-radius: 100px;
    box-shadow: 0px 0px 2px #55acee;
    padding: 20px 20px;
    color: white;
    background-color: rgba(85, 172, 238, 0.2);
    align-self: center;
}
.rounded-card {
    border-radius: 1rem;
}

.text-lg {
    font-size: 1rem;
}
</style>