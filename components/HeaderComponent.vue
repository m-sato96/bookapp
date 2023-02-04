<template>
  <div>
    <v-app-bar app elevate-on-scroll elevation="4" color="teal" dark>
      <v-toolbar-title v-text="title" />
      <v-spacer />
      <v-btn icon @click.stop="rightDrawer = !rightDrawer">
        <v-icon>mdi-menu</v-icon>
      </v-btn>
    </v-app-bar>
    <v-navigation-drawer v-model="rightDrawer" :right="right" temporary fixed>
      <v-list>
        <v-list-item @click.native="routerPush('BookDepository')">
          <v-list-item-action>
            <v-icon light color="amber"> mdi-bookmark </v-icon>
          </v-list-item-action>
          <v-list-item-title>保存した書籍一覧</v-list-item-title>
        </v-list-item>
      </v-list>
      <v-list>
        <v-list-item @click.native="routerPush('SearchBook')">
          <v-list-item-action>
            <v-icon light color="teal"> mdi-bookshelf </v-icon>
          </v-list-item-action>
          <v-list-item-title>書籍一覧</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'BookApp',
    }
  },
  methods: {
    routerPush(link) {
      this.$router.push(`/BookHome/${link}`)
      this.rightDrawer = false
    },
  },
}
</script>
