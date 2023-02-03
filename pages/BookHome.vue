<template>
  <div>
    <NuxtChild
      :books="books"
      @add-book="addBook"
      @update-book-info="updateBookInfo"
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
    addBook(e) {
      this.books.push({
        id: this.books.length + 1,
        image: e.image,
        title: e.title,
        description: e.description,
        readDate: '',
        memo: '',
      })
      this.saveBooks()
      this.goToEditPage(this.books.slice(-1)[0].id)
    },
    updateBookInfo(e) {
      const updateData = {
        id: e.id,
        image: this.books[e.id - 1].image,
        title: this.books[e.id - 1].title,
        description: this.books[e.id - 1].description,
        readDate: e.readDate,
        memo: e.memo,
      }
      this.books.splice(e.id - 1, 1, updateData)
      this.saveBooks()
      this.$router.push('/BookHome/BookDepository')
    },
    saveBooks() {
      const data = JSON.stringify(this.books)
      localStorage.setItem('books', data)
    },
    goToEditPage(id) {
      this.$router.push(`/BookHome/edit/${id}`)
    },
  },
}
</script>

<style></style>
