<template>
  <div id="app">
    <h2>My awesome list</h2>
    <sort-products-list @order-product-list="onOrderProductList"></sort-products-list>
    <product-list :products="products"></product-list>
    <!-- With @ we can listen to add-product event and assign onAddProduct-->
    <add-product @add-product="onAddProduct"></add-product>

  </div>
</template>

<script>
import uuid from "uuid/v4";
import ProductList from './components/ProductList';
import AddProduct from './components/AddProduct';
import SortProductsList from './components/SortProductsList';


export default {
  name: "app",
    components: {
    ProductList,
    AddProduct,
    SortProductsList
  },
  data() {
    return {
      products: [
        {
          id: 0,
          name: "Pizza"
        },
        {
          id: 1,
          name: "Coffee"
        }
      ],
      newProduct: {
        name: ""
      }
    };
  },
    methods: {
    // onSubmit() {
    //   this.$validator.validateAll().then(result => {
    //     if (!result) {
    //       return;
    //     }
    //     //5/ 3. However, they share some common data
    //     this.products.push({
    //       id: uuid(),
    //       ...this.newProduct
    //     });
    //     this.newProduct.name = "";
    //     this.$validator.reset();
    //   });
    // },
    //3/ All we have to do in a method is to add product to the list
    onAddProduct(product) {
      this.products.push(product);
    },

    onOrderProductList() {
      //alert('Order');
      this.products.sort(function(a,b) {return (a.name.toUpperCase() > b.name.toUpperCase()) ? 1 : ((b.name.toUpperCase() > a.name.toUpperCase()) ? -1 : 0);} ); 
      //return _.orderBy(this.products, 'name', 'asc');
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
