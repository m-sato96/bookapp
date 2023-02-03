<template>
  <div class="px-5">
    <h1 class="my-6">保存した書籍</h1>

    <v-row class="mt-6">
      <v-col v-for="book in books" :key="book.id" cols="12" sm="6" md="4">
        <v-card
          :loading="loading"
          class="mx-auto mb-6 card_item pb-5"
          max-width="400"
        >
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
    <v-btn text color="primary" class="mt-5" to="/BookHome/SearchBook">
      <v-icon right dark class="mr-3"> mdi-arrow-left </v-icon>
      書籍一覧に戻る
    </v-btn>
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
