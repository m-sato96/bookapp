<template>
  <div>
    <NuxtChild
      :books="books"
      @detail-book="detailBook"
      @update-book-info="updateBookInfo"
      @books-delete="booksDelete"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      books: [],
    }
  },
  created() {
    if (localStorage.getItem('books')) {
      try {
        this.books = JSON.parse(localStorage.getItem('books'))
      } catch {
        localStorage.removeItem('books')
      }
    }
  },
  methods: {
    detailBook(e) {
      const data = JSON.stringify(e)
      localStorage.setItem('SelectedBooks', data)
      this.$router.push(`/BookHome/edit/${e.id}`)
    },
    updateBookInfo(e) {
      // 保存済みの書籍かどうか
      const isSaved = this.books.some((book) => {
        return e.id === book.id
      })
      if (isSaved) {
        const index = this.books.findIndex((book) => e.id === book.id)
        this.books.splice(index, 1, e)
      } else {
        this.books.push(e)
      }
      this.saveBooks()
      this.$router.push('/BookHome/BookDepository')
    },
    booksDelete() {
      localStorage.setItem('books', '')
      localStorage.removeItem('books')
      this.books = []
    },
    saveBooks() {
      const data = JSON.stringify(this.books)
      localStorage.setItem('books', data)
    },
  },
}
</script>

<style></style>
