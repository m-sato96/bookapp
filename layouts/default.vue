<template>
  <v-app>
    <HeaderComponent />
    <v-main>
      <v-container class="py-10">
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
