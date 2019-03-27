<template>
  <div id="app">
    <header>
      <h3>Subreddit</h3>
    </header>
    <div class="input-con">
      <input type="text" name="new-category" placeholder="Add new Category" v-model="inputValue">
      <button @click="saveCategory">Add</button>
    </div>

    <div class="cover">
      <subreddits v-for="(category,index) in categories" :key="index" :category="category"></subreddits>
      <!-- <subreddits category="space"></subreddits>
        <subreddits category="sports"></subreddits>
        <subreddits category="art"></subreddits>
      <subreddits category="movies"></subreddits>-->
    </div>
  </div>
</template>

<script>
import subreddits from "./components/subreddits";

export default {
  name: "App",
  data() {
    return {
      categories: ["food", "space", "sports", "art", "movies"],
      inputValue: ""
    };
  },
  methods: {
    saveCategory() {
      this.categories.push(this.inputValue);
      // this.categories.sort();
      this.inputValue = "";
    }
  },
  components: {
    subreddits
  }
};
</script>

<style>
body {
  font-family: arial;
  color: #666666;
  background: #f4f4f4;
  margin: 0;
  padding: 0;
  /* display: flex; */
  overflow-x: hidden;
}
::-webkit-scrollbar {
  display: none;
}

::-moz-scrollbar {
  display: none;
}

::-ms-overflow-style {
  display: none;
}

a {
  text-decoration: none;
}
header {
  background: coral;
  color: #ffffff;
  padding: 10px;
  text-align: center;
  width: 100%;
}
.cover {
  display: flex;
  /* flex-direction: row-reverse; */
  flex-wrap: wrap;
  justify-content: space-evenly;
  /* width:100%; */
}
input {
  padding: 10px 20px;
  outline: none;
}
.input-con {
  display: flex;
  justify-content: center;
  margin: 10px 0;
}
button {
  padding: 10px;
  background: coral;
  border: none;
  color: white;
  outline: none;
}
</style>
