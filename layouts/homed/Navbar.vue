<template>
    <v-app-bar
    fixed
    id="rounded-corners"
    color="transparent"
    dark
    :color="appBarColor"
    elevate-on-scroll
    >
    <!-- :class="{ 'onScroll': !view.topOfPage }" -->
        <v-toolbar-title>
            <span class="logo mt-2">
                <img src="~/assets/img/logo/apr.svg" 
                    class="rounded" alt="..."
                    >
            </span>
        </v-toolbar-title>

        <v-spacer></v-spacer>

        <v-btn text to="#Topview" :color="buttonColor">
            Beranda
        </v-btn>
        <v-btn text to="#Middleview" :color="buttonColor">
            Alur Pengajuan
        </v-btn>
        <v-btn text to="#Footerview" :color="buttonColor">
            Tentang Kami
        </v-btn>
    </v-app-bar>
</template>
<script>
export default {
    data() {
        return{
            scrollPosition: null
        }
    },
    methods: {
        updateScroll() {
            this.scrollPosition = window.scrollY
        }
    },
    computed: {
        appBarColor() { return this.scrollPosition > 1 ? 'rgba(255,255,255,1)' : 'rgba(0,0,0,0)'; },
        buttonColor() { return this.scrollPosition > 1 ? 'rgba(0,0,0,1)' : 'rgba(255,255,255,1)'; }
    },
    mounted() {
        window.addEventListener('scroll', this.updateScroll);
    }
}
</script>
<style>
    #rounded-corners {
        border-radius: 0rem 0rem 2rem 2rem;
    }
</style>