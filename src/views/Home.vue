<template>
  <div class="home">
    <h1>{{ message }}</h1>
     <p>Create a new product</p>
          <button v-on:click="addProduct">Add a product</button>
    
    <div v-for="product in products">
      <p>Name: {{product.name}}</p>
      <p>Description: {{product.description}}</p>
      <p>Price: {{product.price}}</p>
      <img v-bind:src="product.image_url">
      <hr>
    </div>
  
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Here Are Some Products!",
      products: [],
    };
  },
  created: function () {
    this.indexProducts();
  },

  methods: {
    indexProducts: function () {
      console.log("printing important stuffs");
      console.log("indexing......");

      axios.get("/api/products").then((response) => {
        console.log(response);
        this.products = response.data;
      });
    },
    addProduct: function () {
      console.log("adding...");

      var params = {
        name: "NEW NEW",
        description: "super new",
        price: 90000,
      };

      axios.post("/api/products", params).then((response) => {
        console.log(response.data);
        this.products.push(response.data);
      });
    },
  },
};
</script>