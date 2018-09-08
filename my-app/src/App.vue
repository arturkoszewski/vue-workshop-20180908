<template>
  <div id="app">
    <h2>My awesome list</h2>
    <input type="text" placeholder="search" v-model="searchText.searchText" v-on:change="onSearchProduct()" />
    <product-list :products="sharedState.products"></product-list>

    <sort-products-list @order-product-list="onOrderProductList"></sort-products-list>
    <!--<product-list :products="products"></product-list> -->
    <add-product @add-product="onAddProduct"></add-product>
  </div>
</template>

<script>
import uuid from "uuid/v4";
import ProductList from './components/ProductList';
import AddProduct from './components/AddProduct';
import SortProductsList from './components/SortProductsList';
//import axios from 'axios';
import store from '../store';


export default {
  name: "app",
    components: {
    ProductList,
    AddProduct,
    SortProductsList
  },

  // async created() {
  //   // 4. products.json has been added to the 'public' directory and it's just an array that we had previously
  //   this.products = await axios.get('products.json').then(res => res.data);
  // },

  created() {
    store.fetchProducts();
  },

  data() {
    // return {
    //   products: [],
    //   newProduct: {
    //     name: ""
    //   }
    // };

    return {
      searchText: { searchText:"" },
      sharedState: store.state
    }
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
    
    //V-1
    // onAddProduct(product) {
    //   this.products.push(product);
    // },

    onAddProduct(product) {
      store.addProduct(product);
    },

    onSearchProduct() {
      var searchText = this.searchText.searchText;
      console.log(searchText);
      store.fetchProducts(searchText);
    },

    onOrderProductList(sortOrder) {
      //console.log(sortOrder);

      if(sortOrder.sortOrder == true) {
        this.products.sort(function(a,b) {return (a.name.toUpperCase() > b.name.toUpperCase()) ? 1 : ((b.name.toUpperCase() > a.name.toUpperCase()) ? -1 : 0);} );
      }
      else {
        this.products.sort(function(a,b) {return (a.name.toUpperCase() < b.name.toUpperCase()) ? 1 : ((b.name.toUpperCase() < a.name.toUpperCase()) ? -1 : 0);} );
      }
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
