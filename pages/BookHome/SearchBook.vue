<template>
  <div>
    <p>book/search</p>
    <v-row align="center">
      <v-col cols="12" sm="6" md="3">
        <v-text-field
          v-model="keyword"
          hide-details="false"
          label="書籍検索"
          outlined
          color="teal"
        ></v-text-field>
      </v-col>
      <v-col cols="12" sm="3" md="3">
        <v-btn
          color="teal"
          class="white--text"
          :disabled="!keyword"
          @click="search(keyword)"
        >
          検索
          <v-icon right dark> mdi-magnify </v-icon>
        </v-btn>
      </v-col>
    </v-row>
    <div v-show="!isFound" class="mt-4 red--text">
      検索に該当する書籍が見つかりませんでした
    </div>

    <v-row class="mt-6">
      <v-col
        v-for="book in searchResults"
        :key="book.id"
        cols="12"
        sm="6"
        md="4"
      >
        <v-card
          :loading="loading"
          class="mx-auto mb-6 card_item pb-5"
          max-width="400"
        >
          <v-img height="200" :src="book.image" contain class="book_img">
            <template v-slot:placeholder>
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
            <div class="book_description">
              {{ book.description }}
            </div>
          </v-card-text>
          <v-card-actions class="plus_btn">
            <v-btn
              class="mx-2"
              fab
              dark
              small
              color="teal"
              @click="addBook(book)"
            >
              <v-icon dark> mdi-plus </v-icon>
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  async asyncData() {
    const baseURL = `https://www.googleapis.com/books/v1/volumes?q="夏目漱石"&maxResults=10`
    const booksData = await fetch(baseURL).then((response) => response.json())
    const getData = booksData.items.map((book) => {
      return {
        id: book.id,
        title: book.volumeInfo.title ? book.volumeInfo.title : '',
        image: book.volumeInfo.imageLinks
          ? book.volumeInfo.imageLinks.thumbnail
          : '/no-image.jpg',
        description: book.volumeInfo.description
          ? book.volumeInfo.description
          : '',
      }
    })
    return { searchResults: getData }
  },
  data() {
    return {
      keyword: '',
      searchResults: [],
      isFound: true,
      loading: false,
    }
  },
  methods: {
    async search(keyword) {
      this.searchResults = []
      const baseURL = `https://www.googleapis.com/books/v1/volumes?q="${keyword}"&maxResults=10`
      const booksData = await fetch(baseURL).then((response) => response.json())
      if (!booksData.items) {
        this.isFound = false
      } else {
        this.searchResults = booksData.items.map((book) => {
          return {
            id: book.id,
            title: book.volumeInfo.title ? book.volumeInfo.title : '',
            image: book.volumeInfo.imageLinks
              ? book.volumeInfo.imageLinks.thumbnail
              : '/no-image.jpg',
            description: book.volumeInfo.description
              ? book.volumeInfo.description
              : '',
          }
        })
      }
    },
    addBook(book) {
      this.$emit('add-book', book)
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
</style>
