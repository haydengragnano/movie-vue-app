<template>
  <div class="movies-new" style="background-color: pink">
    <form v-on:submit.prevent="createMovie()">
      <h1 class="animate__animated animate__slideInLeft animate__infinite infinite">New Movie</h1>
      <img
        src="https://images.unsplash.com/photo-1545630478-cf62cdd247d1?ixid=MnwxMjA3fDB8MHxzZWFyY2h8MjB8fG1vdmllc3xlbnwwfHwwfHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
        alt=""
        width="auto"
        height=""
      />
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newMovieParams.title" />
      </div>
      <div>
        <label>Year:</label>
        <input type="text" v-model="newMovieParams.year" />
      </div>
      <div>
        <label>Director:</label>
        <input type="text" v-model="newMovieParams.director" />
      </div>
      <div>
        <label>Plot:</label>
        <input type="text" v-model="newMovieParams.plot" />
        <br />
        <small>{{ 200 - newMovieParams.plot.length }} characters remaining</small>
      </div>
      <input id="create" type="submit" value="Create" />
    </form>
  </div>
</template>
<style>
label {
  color: purple;
  text-align: left;
  font-size: 20px;
}
small {
  color: blue;
}
#create {
  background-color: green;
  font-size: 10em;
}
h1 {
  --animate-duration: 3s;
}
</style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newMovieParams: {
        plot: "",
      },
      errors: [],
    };
  },
  methods: {
    createMovie: function () {
      axios
        .post("/movies", this.newMovieParams)
        .then((response) => {
          console.log(response.data);
          this.$parent.flashMessage = "Movie successfully created!";
          this.$router.push("/movies");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
