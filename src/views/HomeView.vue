<template>
  <!-- navbar en app.vue -->

  <div class="bg-img">
    <div class="layer">
      <div class="row">
        <div class="col-md-12 text-center">
          <h1>Busca tus peliculas, series <br />de TV y más.</h1>
          <h3>Fácil y rapido con Vueflix.</h3>
          <h5>
            Listo para buscar? Solo ingresa el nombre de la pelicula o serie que quieras ver su descripción.
          </h5>
        </div>
      </div>
      <div class="row w-100">
        <div class="col-md-2 col-1"></div>
        <div class="col-md-8 col-10 p-0 main-search">
          <form @submit.prevent="buscarPeliculas()" class="input-group mb-3">
            <input
              class="form-control"
              type="text"
              placeholder="ejemplo: Batman"
              v-model="buscar"
            />
            <span
              ><input class="input-group-text" type="submit" value="buscar" v-on:click="show = !show"
            /></span>
            <transition name="slide-fade">
    
  </transition>
          </form>
        </div>
        <div class="col-md-2 col-1"></div>
      </div>
    </div>
  </div>

  <section v-if="show">
    <div class="container">
      <div class="row">
        <div
          class="col-lg-6 d-flex justify-content-center"
          v-for="movie in movies"
          :key="movie.imdbID"
        >
        <div class="card my-4">
          <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
            <div class="card-body text-center">
              <div class="card-img py-2">
                <img class="featured-img" :src="movie.Poster" alt="Movie Poster" />
                <div class="type">{{ movie.Type }}</div>
              </div>
              <div class="detail">
                <p class="year">{{ movie.Year }}</p>
                <h3>{{ movie.Title }}</h3>
              </div>
            </div>
          </router-link>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import env from "@/env.js";

export default {
  data() {
    return {
      buscar: "",
      movies: [],
      show:false
    };
  },

  methods: {
    async buscarPeliculas() {
      if (this.buscar != "") {
        try {
          const data = await fetch(
            `http://www.omdbapi.com/?apikey=${env.apikey}&s=${this.buscar}`
          );
          const getPeliculas = await data.json();
          this.movies = getPeliculas.Search;
          console.log(this.movies);
        } catch (error) {
          throw error;
        }
      }
    },
  },
  created() {
    this.buscarPeliculas();
  },
};
</script>

<style>
::-webkit-scrollbar {
  width: 7px;
}
::-webkit-scrollbar-thumb {
  background-color: #e50914;
  border-radius: 5px;
}
::-webkit-scrollbar-track {
  background-color: #222;
}

h1 {
  color: #fff;
  font-size: 80px;
}

h3,
h5 {
  color: #fff;
}

.row {
  margin: 0px;
}
a{
  text-decoration: none !important;
  color: #fff !important;
}
a.navbar-brand {
  color: #e50914 !important;
  font-size: 44px;
  font-weight: bold;
}

.bg-img {
  background-image: url(../assets/banner.png);
  height: 100vh;
}

.layer {
  background-color: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  width: 100%;
  height: 100%;
}

.top-sign-in {
  height: 34px;
  margin-top: 10px;
  padding-top: 5px;
}


.input-group-text{
  font-size: 18px !important;
  background-color: #e50914 !important;
  color: #fff !important;
  border: 0px !important;
  cursor: pointer !important;
}

section {
  border-top: 8px solid #222;
  padding-top: 50px;
  padding-bottom: 40px;
  background-color: #000000;
}
section h2 {
  font-size: 55px;
  color: #fff;
  font-weight: bold;
}

section p {
  font-size: 22px;
  color: #fff;
}

.card {
  background-color: rgba(59, 59, 59, 0.2) !important;
  width: 250px;
  transition: all 0.3s;
}

.card:hover{
  background-color: rgba(80, 80, 80, 0.2) !important;
  transform: translateY(-10px);
} 

.featured-img {
    max-width: 200px;
    margin-bottom: 16px;
  }



.slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}

</style>