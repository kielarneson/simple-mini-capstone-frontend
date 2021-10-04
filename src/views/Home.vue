<template>
  <div class="home">
    <h1>Create New Product</h1>
    <button v-on:click="createProduct()">Create</button>
    <h1>All Products</h1>
    <div v-for="product in products" v-bind:key="product.id">
      <h2>{{ product.name }}</h2>
      <p>{{ product.description }}</p>
      <p>{{ product.price }}</p>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      products: [],
    };
  },
  created: function () {
    this.indexProducts();
  },
  methods: {
    indexProducts: function () {
      axios.get("http://localhost:3000/products").then((response) => {
        this.products = response.data;
        console.log("All products", this.products);
      });
    },
    createProduct: function () {
      var params = {
        name: "Test name",
        description: "Test description",
        price: 1,
        image_url: "Test image.url",
      };
      axios.post("http://localhost:3000/products", params).then((response) => {
        console.log("Success", response.data);
        this.products.push(response.data);
      });
    },
  },
};
</script>
