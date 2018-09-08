<template>
  <form @submit.prevent="onSubmit()">
    <button>Sort</button>
  </form>
</template>

<script>
  export default {
    name: "SortProductsList",
    data() {
      return {
        sortOrder: { sortOrder: true}
      }
    },
    methods: {
      onSubmit() {
          this.$emit('order-product-list', {
            ...this.sortOrder
          });
          this.sortOrder.sortOrder = !this.sortOrder.sortOrder;
        }
    }
  }
</script>

<style scoped>

</style>