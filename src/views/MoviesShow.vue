<template>
  <div class="movies-show">
    <div>
      <h2>Title: {{ movie.title }}</h2>
      <h4>Year: {{ movie.year }}</h4>
      <h4>Plot: {{ movie.plot }}</h4>
      <h4>Director: {{ movie.director }}</h4>
    </div>
    <router-link :to="`/movies/${movie.id}/edit`">Edit</router-link>
    <br />
    <button v-on:click="destroyMovie()">Delete</button>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    axios.get(`/movies/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {
    destroyMovie: function () {
      if (confirm("Are you sure you want to delete this movie?")) {
        axios.delete(`/movies/${this.movie.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        });
      }
    },
  },
};
</script>
