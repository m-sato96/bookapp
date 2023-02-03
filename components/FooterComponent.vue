<template>
  <v-footer :absolute="!fixed" app color="teal" dark>
    <span>&copy; {{ new Date().getFullYear() }} sato</span>
  </v-footer>
</template>

<script>
export default {
  data() {
    return {
      fixed: false,
    }
  },
}
</script>
