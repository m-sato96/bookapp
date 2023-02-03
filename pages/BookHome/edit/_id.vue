<template>
  <div class="px-5">
    <v-btn text color="primary" class="mb-1 pa-0" to="/BookHome/SearchBook">
      <v-icon right dark class="mr-3"> mdi-arrow-left </v-icon>
      書籍一覧に戻る
    </v-btn>
    <h1 class="my-6">{{ book.title }}</h1>
    <div class="mb-5">
      <v-img height="250" :src="book.image" contain class="book_img">
        <template #placeholder>
          <v-row class="fill-height ma-0" align="center" justify="center">
            <v-progress-circular
              indeterminate
              color="grey lighten-5"
            ></v-progress-circular>
          </v-row>
        </template>
      </v-img>
    </div>
    <p>{{ book.description }}</p>
    <v-col cols="12" sm="6" md="4">
      <v-menu
        v-model="menu"
        :close-on-content-click="false"
        :nudge-right="40"
        transition="scale-transition"
        offset-y
        min-width="auto"
      >
        <template #activator="{ on, attrs }">
          <v-text-field
            v-model="date"
            color="teal"
            label="読んだ日"
            prepend-icon="mdi-calendar"
            readonly
            v-bind="attrs"
            v-on="on"
          ></v-text-field>
        </template>
        <v-date-picker
          v-model="date"
          color="teal"
          locale="jp-ja"
          :day-format="(date) => new Date(date).getDate()"
          @input="menu = false"
        ></v-date-picker>
      </v-menu>
    </v-col>
    <v-textarea
      v-model="book.memo"
      outlined
      label="メモ"
      value="{book.memo}"
      color="teal"
    ></v-textarea>
    <div class="text-center">
      <v-btn x-large color="teal" dark @click="updateBookInfo">
        保存する
      </v-btn>
    </div>
  </div>
</template>

<script>
export default {
  beforeRouteEnter(to, from, next) {
    next((vm) => {
      vm.book = JSON.parse(localStorage.getItem('SelectedBooks'))
      if (vm.book.readDate) {
        vm.date = vm.book.readDate
      } else {
        vm.date = new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
          .toISOString()
          .substr(0, 10)
      }
    })
  },
  data() {
    return {
      book: {},
      date: '',
      menu: false,
    }
  },
  methods: {
    updateBookInfo() {
      this.$emit('update-book-info', {
        ...this.book,
        readDate: this.date,
        memo: this.book.memo,
      })
    },
  },
}
</script>

<style scoped>
.book_img {
  background: #dce3dd;
}
h1 {
  font-size: 25px;
}
</style>
