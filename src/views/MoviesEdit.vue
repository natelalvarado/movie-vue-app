<template>
  <div class="movies-edit">
    <form v-on:submit.prevent="editMovie()">
      <h1>Edit Movie</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        Title:
        <input type="text" v-model="editMovieParams.title" />
      </div>
      <div>
        Year:
        <input type="text" v-model="editMovieParams.year" />
      </div>
      <div>
        Plot:
        <input type="text" v-model="editMovieParams.plot" />
      </div>
      <div>
        Director:
        <input type="text" v-model="editMovieParams.director" />
      </div>
      <input type="submit" value="Update" />
    </form>
    editMovieParams: {{ editMovieParams }}
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      editMovieParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get(`/movies/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.editMovieParams = response.data;
    });
  },
  methods: {
    editMovie: function () {
      axios
        .patch(`/movies/${this.editMovieParams.id}`, this.editMovieParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push(`/movies/${response.data.id}`);
        })
        .catch((error) => {
          console.log(error.response.data.errors);
        });
    },
  },
};
</script>
