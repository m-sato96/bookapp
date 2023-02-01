<template>
  <v-app>
    <HeaderComponent />
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <FooterComponent />
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {}
  },
}
</script>
