<template>
  <div class="movies-index" style="background-color: #adb5bd">
    <div class="container">
      <div class="card" style="width: 18rem"></div>
      <h1 class="animate__animated animate__slideInLeft animate__infinite infinite">Movies!</h1>
      Search by title:
      <input v-model="titleFilter" list="titles" />
      <datalist id="titles">
        <option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
      </datalist>
      <div>
        <button class="btn btn-info" type="button" v-on:click="setSortAttribute('title')">
          Sort Title
          <span v-if="sortOrder === 1 && sortAttribute === 'title'">^</span>
          <span v-if="sortOrder === -1 && sortAttribute === 'title'">v</span>
        </button>
        <button class="btn btn-info ms-3" type="button" v-on:click="setSortAttribute('year')">
          Sort Prep Time
          <span v-if="sortOrder === 1 && sortAttribute === 'year'">^</span>
          <span v-if="sortOrder === -1 && sortAttribute === 'year'">v</span>
        </button>
      </div>

      <div
        class="card-body"
        v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), sortAttribute, sortOrder)"
        v-bind:key="movie.id"
      >
        <div class="card" style="width: 18rem">
          <h4>{{ movie.title }}</h4>
          <img :src="movie.image" alt="" />
          <p>Year: {{ movie.year }}</p>
          <router-link :to="`/movies/${movie.id}`">See Details</router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
h1 {
  color: red;
}
</style>

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
