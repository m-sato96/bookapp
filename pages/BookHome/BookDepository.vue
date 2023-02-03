<template>
  <div class="px-5">
    <v-btn text color="primary" class="mb-1 pa-0" to="/BookHome/SearchBook">
      <v-icon right dark class="mr-3"> mdi-arrow-left </v-icon>
      書籍一覧に戻る
    </v-btn>
    <h1 class="my-6">保存した書籍</h1>
    <div v-if="books.length">
      <v-row class="mt-6">
        <v-col v-for="book in books" :key="book.id" cols="12" sm="6" md="4">
          <v-card class="mx-auto mb-6 card_item pb-5" max-width="400">
            <v-img height="200" :src="book.image" contain class="book_img">
              <template #placeholder>
                <v-row class="fill-height ma-0" align="center" justify="center">
                  <v-progress-circular
                    indeterminate
                    color="grey lighten-5"
                  ></v-progress-circular>
                </v-row>
              </template>
            </v-img>
            <v-card-title>{{ book.title }}</v-card-title>
            <v-card-text>
              <div class="book_description mb-2">
                {{ book.description }}
              </div>
              <div>
                <p class="mb-0 teal--text">メモ</p>
                <p class="black--text mb-0">{{ book.memo }}</p>
              </div>
              <p v-if="book.readDate" class="teal--text read_date">
                読んだ日: {{ book.readDate }}
              </p>
            </v-card-text>

            <v-card-actions class="plus_btn">
              <v-btn
                class="mx-2"
                fab
                dark
                small
                color="teal"
                :to="`/BookHome/edit/${book.id}`"
              >
                <v-icon dark> mdi-pencil </v-icon>
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
      <v-btn color="red lighten-2 mt-16" dark @click.stop="dialog = true">
        保存した書籍の一括削除
      </v-btn>

      <v-dialog v-model="dialog" max-width="290">
        <v-card>
          <v-card-title> 保存済みの全ての書籍を削除しますか？ </v-card-title>
          <v-card-actions>
            <v-spacer></v-spacer>

            <v-btn color="green darken-1" text @click="dialog = false">
              いいえ
            </v-btn>

            <v-btn color="green darken-1" text @click="booksDelete">
              はい
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </div>
    <div v-else class="text-center text--h6 my-16 grey--text">
      保存した書籍はありません
    </div>
  </div>
</template>

<script>
export default {
  props: {
    books: {
      type: Array,
      default: () => {},
    },
  },
  data() {
    return {
      dialog: false,
    }
  },
  methods: {
    booksDelete() {
      this.$emit('books-delete')
    },
  },
}
</script>

<style scoped>
.card_item {
  height: 100%;
}
.book_description {
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
  overflow: hidden;
}
.book_img {
  background: #dce3dd;
}
.plus_btn {
  position: absolute;
  bottom: 8px;
  right: 0;
}
.read_date {
  position: absolute;
  bottom: 8px;
  left: 16px;
}
</style>
