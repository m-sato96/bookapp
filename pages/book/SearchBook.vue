<template>
  <div>
    <p>book/search</p>
    <v-row align="center">
      <v-col cols="12" sm="6" md="3">
        <v-text-field
          v-model="keyword"
          hide-details="false"
          label="Outlined"
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
          class="mx-auto mb-6 card_item"
          max-width="400"
        >
          <v-img height="200" :src="book.image" contain></v-img>
          <v-card-title>{{ book.title }}</v-card-title>

          <v-card-text>
            <div class="book_description">
              {{ book.description }}
            </div>
          </v-card-text>

          <v-card-actions>
            <v-btn color="deep-purple lighten-2" text @click="reserve">
              Reserve
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  data() {
    return {
      keyword: '',
      searchResults: [],
      isFound: true,
      loading: false,
      selection: 1,
    }
  },
  methods: {
    async search(keyword) {
      this.searchResults = []
      const baseURL = `https://www.googleapis.com/books/v1/volumes?q=${keyword}&maxResults=10`
      const booksData = await fetch(baseURL).then((response) => response.json())
      if (booksData.items === 'undefined') {
        this.isFound = false
        return
      }
      this.searchResults = booksData.items.map((book) => {
        return {
          id: book.id,
          title: book.volumeInfo.title ? book.volumeInfo.title : '',
          image: book.volumeInfo.imageLinks.thumbnail
            ? book.volumeInfo.imageLinks.thumbnail
            : '',
          description: book.volumeInfo.description
            ? book.volumeInfo.description.slice(0, 100)
            : '',
        }
      })
      console.log('this.searchResult')
      console.log(this.searchResults)
    },
    reserve() {
      this.loading = true

      setTimeout(() => (this.loading = false), 2000)
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
</style>
