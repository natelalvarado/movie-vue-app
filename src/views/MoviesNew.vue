<template>
  <div class="movies-new">
    <form v-on:submit.prevent="createMovie()">
      <h1>New Movie</h1>
      <div>
        Title:
        <input type="text" v-model="newMovieParams.title" />
      </div>
      <div>
        Year:
        <input type="text" v-model="newMovieParams.year" />
      </div>
      <div>
        Plot:
        <input type="text" v-model="newMovieParams.plot" />
      </div>
      <div>
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
      newMovieParams: {},
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
