<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p>{{ message2 }}</p>
    <h2>{{ addThree(numbers) }}</h2>
  </div>
</template>

<style></style>

<script>
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      numbers: [1, 6, 9],
    };
  },
  created: function () {},
  methods: {
    addThree: function (array) {
      var index = 0;
      var newNumbers = [];

      while (index < array.length) {
        newNumbers.push(array[index] + 3);
        index += 1;
      }
      return newNumbers;
    },
  },
};
</script>
