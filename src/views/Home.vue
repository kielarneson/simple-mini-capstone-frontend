<template>
  <div class="home">
    <div>
      <h1>Create New Product</h1>
      <div>
        Name:
        <input type="text" v-model="newProductParams.name" />
      </div>
      <div>
        Description:
        <input type="text" v-model="newProductParams.description" />
      </div>
      <div>
        Price:
        <input type="text" v-model="newProductParams.price" />
      </div>
      <div>
        Image URL:
        <input type="text" v-model="newProductParams.image_url" />
      </div>
      <button v-on:click="createProduct()">Create</button>
    </div>
    <h1>All Products</h1>
    <div v-for="product in products" v-bind:key="product.id">
      <h2>{{ product.name }}</h2>
      <p>{{ product.description }}</p>
      <img :src="product.image_url" alt="" />
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
      newProductParams: {},
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
      axios.post("http://localhost:3000/products", this.newProductParams).then((response) => {
        console.log("Success", response.data);
        this.products.push(response.data);
        this.newProductParams = {};
      });
    },
  },
};
</script>
