<template>
    <v-app>
        <Navbar/>
        <TopviewVue />
        <MiddleviewVue />
        <FooterviewVue />
    </v-app>
</template>
<script>
import TopviewVue from './homed/Topview.vue';
import MiddleviewVue from './homed/Middleview.vue';
import FooterviewVue from './homed/Footerview.vue';
import Navbar from './homed/Navbar.vue';
export default {
    name: 'homed',
    components: {
    TopviewVue,
    MiddleviewVue,
    FooterviewVue,
    Navbar
}
}
</script>
<style>
    
</style>