<template>
    <div>
        <div class="container">

            <nav
            class="navbary fixed-top navbar-expand-lg pt-2 pb-2"
            data-aos="fade-down"
            data-aos-duration="1000"
            :class="{ onScroll: !view.topOfPage }"
                >
                    <div class="container d-flex ">
                            <div class="col">
                                <a class="navbar-brandy fs-4" href="#" :class="{ 'onScroll': !view.topOfPage}"                        >
                                    <span class="logo">
                                        <img src="~/assets/img/logo/apr.svg" 
                                            class="rounded" alt="..."
                                            >
                                    </span>
                                </a>
                            </div>                    
                            <div class="collapse navbar-collapse justify-content-center" id="navbarSupportedContent">
                                <ul class="navbar-nav">
                                    <div class="col-md-4">         
                                    <li class="nav-item"><a class="nav-linky fs-5" :class="{ 'onScroll': !view.topOfPage}" href="#myCarousel">Beranda</a></li>                
                                    </div>
                                    <div class="col-md-6">
                                    <li class="nav-item"><a class="nav-linky fs-5" :class="{ 'onScroll': !view.topOfPage}" href="#body">Alur Pengajuan</a></li>
                                    </div>
                                    <div class="col-md-6">
                                    <li class="nav-item"><a class="nav-linky fs-5" :class="{ 'onScroll': !view.topOfPage}" href="#FooterView">Tentang Kami</a></li>
                                    </div>
                                </ul>
                            </div>
                            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                                <span class="navbar-toggler-icon"><i class="fas fa-bars fas-color" :class="{ 'onScroll': !view.topOfPage}"></i></span>
                            </button>
                    </div>
    
                </nav>
        </div>
        <TopView />
        <MiddleView />
        <FooterView />
    </div>
</template>

<style >
    @import "https://pro.fontawesome.com/releases/v5.10.0/css/all.css";
    @import '~/assets/css/app.css';
</style>

<script>
import FooterView from './home/FooterView.vue'
import MiddleView from './home/MiddleView.vue'
// import NavBar from './home/NavBar.vue'
import TopView from './home/TopView.vue'

// import aos from '~/plugins/aos'
// import AOS from 'aos'
import 'aos/dist/aos.css'

export default {
    name: 'home',
    // mixins:[aos],
    components: {
        // NavBar,
        TopView,
        MiddleView,
        FooterView,
        // Home,
    },
    data () {
        return {
            view: {
                topOfPage: true
            }
        }
    },
    beforeMount() {
        window.addEventListener('scroll', this.handleScroll)
    },
    methods: {
        handleScroll(){
            if(window.pageYOffset>0){
                if(this.view.topOfPage) this.view.topOfPage = false
            } else {
                if(!this.view.topOfPage) this.view.topOfPage = true
            }
        }
    },
    head () {
        return {
        title: 'APR',
        link: [
            { rel: 'stylesheet', href: '/bootstrap/css/bootstrap.min.css' }
        ],
        script: [
            { src: "/bootstrap/js/bootstrap.min.js", type: "text/javascript"},
            { src: "/bootstrap/umd/popper.min.js", type: "text/javascript"},
        ]

        }
    },
    // created ( ) {
    //     AOS.init()
    //     AOS.refresh()
    // },
    async mounted() {
    const AOS = await import('aos');
    AOS.init();
    }
    // created() { setTimeout(function () { document.querySelectorAll('.aos-animate').forEach(item => { item.classList.remove("aos-animate"); setTimeout( function (){ window.scrollTo(0, 2); },600) }) },50,this) }, beforeRouteLeave (to, from, next) { next(); window.scrollTo(0, 0); document.querySelectorAll('.aos-animate').forEach(item => { item.classList.remove("aos-animate"); }) }, beforeRouteEnter (to, from, next) { next(); window.scrollTo(0, 0); } 
}
</script>
