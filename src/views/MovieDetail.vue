<template>

<div class="movie-detail">
    <h2>{{movie.Title}}</h2>
    <p>{{ movie.Year }}</p>
    <img :src="movie.Poster" alt="Movie Poster" class="featured-img" />
    <p>{{ movie.Plot }}</p>
  </div>

  
</template>

<script>
import env from '@/env.js'


export default {
  data(){
  return{
    movie:{},
    
  };
},

methods:{
  async buscarPelicula(){
    if (this.buscar != "") {   
         try {
        const data = await fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${this.$route.params.id}&plot=full`);
        const getPelicula = await data.json();
        this.movie = getPelicula;
        console.log(this.movie);
      } catch (error) {
        throw error;
      }  
           
  }
}
},
created() {
    this.buscarPelicula();
  },

}




</script>

<style lang="scss" scoped>

.movie-detail {
  border-top: 8px solid #222;
   padding-top: 75px;
   //padding-bottom: 66px;
   padding-left: 50px;
   padding-right: 50px;
   background-color: #000000;
   height: 100vh;
  h2 {
    font-size: 55px;
   color: #fff;
   font-weight: bold;
  }
  .featured-img {
    display: block;
    max-width: 200px;
    margin-bottom: 16px;
  }
  p {
     font-size: 18px;
   color: #fff;
  }
}
</style>