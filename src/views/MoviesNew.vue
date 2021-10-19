<template>
  <div class="movies-new">
    <form v-on:submit.prevent="createMovie()">
      <h1 style="color: white; background-color: #986fda; font-family: georgia">
        New Movie
      </h1>
      <div style="font-family: georgia">
        Title:
        <input type="text" v-model="newMovieParams.title" />
      </div>
      <div style="font-family: georgia">
        Year:
        <input type="text" v-model="newMovieParams.year" />
      </div>
      <div style="font-family: georgia">
        Plot:
        <input type="text" v-model="newMovieParams.plot" />
        <br />
        <small
          >Remaining Characters: {{ 200 - newMovieParams.plot.length }}</small
        >
      </div>
      <div style="font-family: georgia">
        Director:
        <input type="text" v-model="newMovieParams.director" />
      </div>
      <input type="submit" value="Create" />
    </form>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newMovieParams: {
        title: "",
        plot: "",
      },
      errors: [],
    };
  },
  created: function () {},
  methods: {
    createMovie: function () {
      axios
        .post("/movies", this.newMovieParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        })
        .catch((error) => {
          console.log(error.response.data.errors);
        });
    },
  },
};
</script>
