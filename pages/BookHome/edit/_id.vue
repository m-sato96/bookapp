<template>
  <div>
    book/edit/_{{ $route.params.id }}
    {{ book }}
  </div>
</template>

<script>
export default {
  beforeRouteEnter(to, from, next) {
    next((vm) => {
      vm.book = vm.books[vm.$route.params.id - 1]
    })
  },
  props: {
    books: {
      type: Array,
      default: () => {},
    },
  },
  data() {
    return {
      book: {},
    }
  },
}
</script>

<style></style>
