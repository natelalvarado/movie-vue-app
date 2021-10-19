<template>
  <div class="movies-index">
    <h1
      style="color: white; background-color: #18a453; font-family: comic-sans"
    >
      All Movies
    </h1>
    Search by title:
    <input v-model="titleFilter" list="titles" />
    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">
        {{ movie.title }}
      </option>
    </datalist>
    <div>
      <button
        style="
          background-color: #ddd;
          border: none;
          color: black;
          padding: 10px 20px;
          text-align: center;
          text-decoration: none;
          display: inline-block;
          margin: 4px 2px;
          cursor: pointer;
          border-radius: 16px;
        "
        v-on:click="setSortAttribute('title')"
      >
        Sort Alphabetically
      </button>
    </div>

    <div
      v-for="movie in orderBy(
        filterBy(movies, titleFilter, 'title'),
        sortAttribute,
        sortOrder
      )"
      v-bind:key="movie.id"
    >
      <h2 style="font-family: georgia">{{ movie.title }}</h2>
      <p style="font-family: georgia">Year: {{ movie.year }}</p>
      <p style="font-family: georgia">Plot: {{ movie.plot }}</p>
      <p style="font-family: georgia">Director: {{ movie.director }}</p>
      <router-link :to="`/movies/${movie.id}`">See Details</router-link>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      movies: [],
      titleFilter: "",
      sortAttribute: "title",
      sortOrder: 1,
    };
  },
  created: function () {
    axios.get("/movies").then((response) => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {
    setSortAttribute: function (attribute) {
      if (this.sortAttribute === attribute) {
        this.sortOrder = this.sortOrder * -1;
      } else {
        this.sortAttribute = attribute;
        this.sortOrder = 1;
      }
    },
  },
};
</script>
