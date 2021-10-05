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
      <div>
        <button v-on:click="showProduct(product)">More Info</button>
      </div>
    </div>

    <dialog id="product-details">
      <form method="dialog">
        <h1>Product info</h1>
        Name:
        <input type="text" v-model="currentProduct.name" />
        Description:
        <input type="text" v-model="currentProduct.description" />
        Price:
        <input type="text" v-model="currentProduct.price" />
        <button v-on:click="updateProduct(currentProduct)">Update</button>
        <button v-on:click="deleteProduct(currentProduct)">Delete</button>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<style>
img {
  width: 550px;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      products: [],
      newProductParams: {},
      currentProduct: {},
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
      axios
        .post("http://localhost:3000/products", this.newProductParams)
        .then((response) => {
          console.log("Success", response.data);
          this.products.push(response.data);
          this.newProductParams = {};
        })
        .catch((error) => console.log(error.response));
    },
    showProduct: function (product) {
      console.log(product);
      this.currentProduct = product;
      document.querySelector("#product-details").showModal();
    },
    updateProduct: function (product) {
      var editProductParams = product;
      axios.patch("http://localhost:3000/products/" + product.id, editProductParams).then((response) => {
        console.log("Success", response.data);
      });
    },
    deleteProduct: function (product) {
      axios.delete(`http://localhost:3000/products/${product.id}`).then((response) => {
        console.log("Product successfully deleted", response.data);
        var index = this.products.indexOf(product);
        this.products.splice(index, 1);
      });
    },
  },
};
</script>
