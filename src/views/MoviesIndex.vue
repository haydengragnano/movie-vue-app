<template>
  <div class="movies-index">
    <h1>All Movies</h1>
    Search by title:
    <input v-model="titleFilter" list="titles" />
    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
    </datalist>
    <div>
      <button v-on:click="setSortAttribute('title')">
        Sort by title
        <span v-if="sortOrder === 1 && sortAttribute === 'title'">^</span>
        <span v-if="sortOrder === -1 && sortAttribute === 'title'">v</span>
      </button>
      <button v-on:click="setSortAttribute('year')">
        Sort by year
        <span v-if="sortOrder === 1 && sortAttribute === 'year'">^</span>
        <span v-if="sortOrder === -1 && sortAttribute === 'year'">v</span>
      </button>
    </div>

    <div
      v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), sortAttribute, sortOrder)"
      v-bind:key="movie.id"
    >
      <h4>{{ movie.title }}</h4>
      <p>Title: {{ movie.title }}</p>
      <p>Year: {{ movie.year }}</p>
      <p>Director: {{ movie.director }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <router-link :to="`/movies/${movie.id}`">See Details</router-link>
    </div>
  </div>
</template>

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
