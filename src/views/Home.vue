<template>
  <div class="home">
    <h1>New Movie</h1>
    <div>Title: <input type="text" v-model="newMovieParams.title" /></div>
    <div>Year: <input type="text" v-model="newMovieParams.year" /></div>
    <div>Plot: <input type="text" v-model="newMovieParams.plot" /></div>
    <div>Director: <input type="text" v-model="newMovieParams.director" /></div>
    <p>newMovieParams: {{ newMovieParams }}</p>
    <button v-on:click="createMovie()">Add New Movie</button>
    <h1>All Movies</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>Title: {{ movie.title }}</h2>
      <p>Year: {{ movie.year }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <p>Director: {{ movie.director }}</p>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: [],
      newMovieParams: {},
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("http://localhost:3000/movies").then((response) => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
    createMovie: function () {
      console.log(this.newMovieParams);
      axios
        .post("http://localhost:3000/movies", this.newMovieParams, {
          headers: {
            Authorization:
              "Bearer eyJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoxLCJleHAiOjE2MzMxMzk3ODB9.WXVnCZ3GgQ3SWu7VG5TPz6n8ZmiGSniSjhN4lYXUuzM",
          },
        })
        .then((response) => {
          console.log(response.data);
          this.recipes.push(response.data);
        })
        .catch((error) => {
          console.log(error.response.data.errors);
        });
    },
  },
};
</script>
