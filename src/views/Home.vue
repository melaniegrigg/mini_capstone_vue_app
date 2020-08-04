<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h1>{{ products }}</h1>

    <div v-for="product in products">
      <p>Name: {{product.name}}</p>
      <p>Description: {{product.description}}</p>
      <p>Price: {{product.price}}</p>
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
      message: "Welcome to Vue.js!",
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
  },
};
</script>