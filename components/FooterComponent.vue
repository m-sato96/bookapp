<template>
  <v-footer dark padless>
    <v-card class="flex" flat tile>
      <v-card-title class="teal">
        <strong class="subheading"
          >Get connected with us on social networks!</strong
        >

        <v-spacer></v-spacer>
        <div v-for="(icon, index) in icons" :key="index">
          <v-btn class="mx-4" dark icon :href="`${icon.path}`" target="_blank">
            <v-icon size="24px">
              {{ icon.name }}
            </v-icon>
          </v-btn>
        </div>
      </v-card-title>

      <v-card-text class="py-2 white--text text-center">
        {{ new Date().getFullYear() }} — <strong>Sato</strong>
      </v-card-text>
    </v-card>
  </v-footer>
</template>

<script>
export default {
  data() {
    return {
      icons: [
        {
          name: 'mdi-github',
          path: 'https://github.com/m-sato96',
        },
      ],
    }
  },
}
</script>
