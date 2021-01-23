<template>
<section>
  <h1>Recipe App</h1>
  <input type="text" placeholder="Search recipes" v-on:keyup="search">
  <ul>
    <li v-for="recipe in getRecipes" :key="recipe">
    <img :src="recipe.recipe.image"/>
    <h3>Title: {{recipe.recipe.label}}</h3>
    <p>Calories:{{recipe.recipe.calories}}</p>
    <p>Total time:{{recipe.recipe.totalTime}}</p>
    <a :href="recipe.recipe.url" target="_blank">View Recipe</a>
    </li>
  </ul>
  </section>
</template>

<script>
export default {
  data(){
    return{
      searchText:"",
      recipes:[],
      appId: "84e00734",
      appkey: "af522918169810286895a0adeee4f50c",
    }
  },
  computed:{
    getRecipes(){
      return this.recipes.filter((recipe) =>{
        return recipe.recipe.label.toLowerCase().match(this.searchText.toLowerCase());
      });
    }
  },
   methods:{
    search(e){
     this.searchText = e.target.value;
       fetch(`https://api.edamam.com/search?q=${this.searchText}&app_id=${this.appId}&app_key=${this.appkey}`)
       .then(result => {
        return result.json();
      }).then(data =>{
       this.recipes = data.hits;
       console.log(this.recipes);
     })
    }
  }
};
</script>

<style>
*{
  margin:0px;
  padding:0px;
  box-sizing:border-box;
}
body{
  background-color:#221e1e;
}
section{
display:block;
margin:0px auto;
width:70%;
}
h1{
  color:white;
  text-align:center;
  padding: 30px;
}
input{
    margin-bottom: 30px;
width: 400px;
font-size:16px;
margin-top:50px;
padding:10px;
display:block;
margin:0px auto;

}
ul{
    margin-top: 30px;
display:flex;
color:white;
list-style:none;
flex-wrap: wrap;
padding: 5px;
}
li{
  border:1px solid white;
  padding:10px;

}
img{
padding: 5px;
}
h3{
  width:280px;
}
p{
  margin-top: 5px;
  margin-bottom: 10px;
}
a{
  text-decoration: none;
  color:white;
  border:1px solid white;
  padding:5px;
   margin-top: 20px;
   background-color:maroon;
}
</style>
