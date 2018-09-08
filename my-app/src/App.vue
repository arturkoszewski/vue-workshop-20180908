<!--10- 1. There's a <template> part -->
<template>
  <div id="app">
    <h2>My awesome list</h2>
    <ul>
      <li v-for="p in products" :key="p.id">{{ p.name }}</li>
    </ul>
    <p v-if="!products.length">No products!</p>
    <button v-on:click="removeLast()">Remove last item</button>
    <br/>

    <form @submit.prevent="onSubmit()">
      <input 
        name="product"
        v-model="newProduct.name" placeholder="new item" 
        v-validate="'required|min:3'"
      />
      <button>Add item from input</button>
      <div v-show="errors.has('product')">
        {{ errors.first('product') }}
      </div>
    </form>

    <form id="orderList" @submit.prevent="onOrderSubmit()">
      <p>Order</p>
      <input 
        name="productOrdered"
        v-model="newProductOrdered.name" placeholder="item to order" 
        v-validate="'included:Coffee,Pizza'"
      />
      <button>Add item to order</button>
      <div v-show="errors.has('productOrdered')">
        {{ errors.first('productOrdered') }}
      </div>
    </form>

  </div>
</template>

<!--21- 2. A <script> part -->
<script>
import uuid from 'uuid/v4';
// 4. Now App is not mounted itself, we're just creating a component (more on that later - hold your horses!)
export default {
  name: 'app',
  //11/ 5. Data can no longer be just an object to prevent accidental shared state
  data() {
    return {
      products: [{
        id: 0,
        name: 'Coffee'
      }, {
        id: 1,
        name: 'Pizza'
      }],

      newProduct:{
        name: ''
      },

      orders:[{
        id:0,
        product:{name:'Prod ord'}
      }],

      newProductOrdered:{
        name: ''
      },

    }
  },
  methods: {
    removeLast() {
      this.products.pop();
    },

    onSubmit() {
      // 3. On the JS side we need to use yet another injected value called $validator to validate all the fields
      this.$validator.validateAll().then(result => {
        if (!result) {
          return;
        }
        this.products.push({
          id: uuid(),
          ...this.newProduct
        });
        this.newProduct.name = '';
        // 4/ and reset validation state after adding a product
        this.$validator.reset();
      });
    },

    onOrderSubmit() {
      var x = true;
    }


  }
}
</script>

<!--9- 3. And <style> part -->
<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
