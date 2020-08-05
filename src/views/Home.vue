<template>
  <div class="home">
    <h1>{{ message }}</h1>
     <p>Create a new product</p>
     <p>Name:<input v-model="newProductName" type="text"></p>
     <p>Description:<input v-model="newProductDescription" type="text"></p>
     <p>Price:<input v-model="newProductPrice" type="text"></p>
     <p>Image:<input v-model="newProductImage" type="text"></p>
          <button v-on:click="addProduct">Add a product</button>
    
    <div v-for="product in products">
      <p>Name: {{product.name}}</p>
      <!-- <p>Description: {{product.description}}</p>
      <p>Price: {{product.price}}</p> -->
      <!-- <p>Image_url: {{product.image_url}}</p> -->
      <img v-bind:src="product.image_url">
      <button v-on:click="showInfo(product)">Show more info</button>
      <hr>
    </div>
  
    <dialog id="product-details">
      <form method="dialog">
        <h1>Product info</h1>
        <p>Name: {{currentProduct.name}}</p>
        <p>Description: {{currentProduct.description}}</p>
        <p>Price: {{currentProduct.price}}</p>
        <button>Close</button>
      </form>
    </dialog>

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
      newProductName: "",
      newProductPrice: "",
      newProductDescription: "",
      newProductImage: "",
      currentProduct: {},
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
      console.log(this.newProductName);

      var params = {
        name: this.newProductName,
        description: this.newProductDescription,
        price: this.newProductPrice,
        image: this.newProductImage,
      };

      axios.post("/api/products", params).then((response) => {
        console.log(response.data);
        this.products.push(response.data);
      });
    },
    showInfo: function (product) {
      console.log(product);
      this.currentProduct = product;
      document.querySelector("#product-details").showModal();
    },
  },
};
</script>