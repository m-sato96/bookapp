<template>
  <div>
    <NuxtChild :books="books" @add-book="addBook" />
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
        readData: '',
        memo: '',
      })
      this.saveBooks()
      this.goToEditPage(this.books.slice(-1)[0].id)
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
