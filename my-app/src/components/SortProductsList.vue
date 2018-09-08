<template>
  <form @submit.prevent="onSubmit()">
    <button>Sort</button>
  </form>
</template>

<script>
  export default {
    name: "SortProductsList",
    //6/ newProduct goes to AddProduct component
    data() {
      return {
        sortOrder: {
          order: 'asc'
        }
      }
    },
    //3/ As well as onSubmit
    methods: {
      onSubmit() {
          this.$emit('order-product-list', {
            ...this.sortOrder
          });
        }
    }
  }
</script>

<style scoped>

</style>