<template>
  <div id="app">
    <header>
      <h3>Subreddit</h3>
    </header>
    <div class="input-con">
      <input type="text" name="new-category" placeholder="Search Category" v-model="inputValue">
     
      <button @click="saveCategory" >Add</button>
    </div>
 <p ref="errormessage">this category doesn't exist...</p>
    <div class="cover">
      <subreddits v-for="(category,index) in categories" :key="index" :category="category"></subreddits>
    </div>
  </div>
</template>

<script>
import subreddits from "./components/subreddits";

export default {
  name: "App",
  data() {
    return {
      categories: [],
      inputValue: "",
      
    };
  },
  methods: {
    saveCategory() {
         this.$refs.errormessage.style.display = "block";
         this.$http.get('https://www.reddit.com/r/' + this.inputValue + '/top.json?limit=5')
            .then((response)=> {
             
                if(response.ok === true){
                     this.$refs.errormessage.style.display = "none";
                     this.categories.push(this.inputValue);
                     console.log(this.inputValue);
                      this.inputValue = "";
                }
            });
    },
 
  },
  components: {
    subreddits
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Courgette');
body {
  font-family: arial;
  color: #666666;
  background: #f4f4f4;
  margin: 0;
  padding: 0;
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
p{
  color:red;
  text-align:center;
  display:none;
  font-family: 'Courgette', cursive;
  font-size:18px;
}
</style>
