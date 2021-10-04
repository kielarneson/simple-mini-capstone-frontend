<template>
  <div class="home">
    <h1>All Recipes</h1>
    <div v-for="recipe in recipes" v-bind:key="recipe.id">
      <h2>{{ recipe.title }}</h2>
      <p>{{ recipe.chef }}</p>
    </div>
  </div>
</template>

<style></style>

<script>
export default {
  data: function () {
    return {
      recipes: [
        { id: 1, chef: "Kiel Arneson", title: "Egg Salad" },
        { id: 2, chef: "Peter Jang", title: "Bison Steak" },
        { id: 3, chef: "Will Wade", title: "Club Sandwich" },
      ],
    };
  },
  created: function () {},
  methods: {},
};
</script>
