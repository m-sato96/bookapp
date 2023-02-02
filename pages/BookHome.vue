<template>
  <div>
    <NuxtChild @add-book="addBook" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      books: [],
    }
  },
  mounted() {
    if (localStorage.getItem('books')) {
      try {
        this.books = JSON.parse(localStorage.getItem('books'))
        console.log(this.books)
      } catch {
        localStorage.removeItem('books')
      }
    }
  },
  methods: {
    addBook(e) {
      this.books.push({
        id: e.id,
        image: e.image,
        title: e.title,
        readData: '',
        memo: '',
      })
      this.saveBooks()
    },
    saveBooks() {
      const data = JSON.stringify(this.books)
      localStorage.setItem('books', data)
    },
  },
}
</script>

<style></style>
