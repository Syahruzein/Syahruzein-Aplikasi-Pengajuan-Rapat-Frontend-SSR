<template>
  <Nuxt/>
</template>

<script>
export default {
  layout: "homed",
  name: 'IndexPage',
  computed: {
    currentUser() {
      return this.$store.state.authentication.user;
    }
  },
  mounted () {
    if (!this.currentUser) {
      this.$router.push('/')
    }
  },
}
</script>
