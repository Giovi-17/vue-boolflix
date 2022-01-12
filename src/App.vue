<template>
  <div id="app">

    <header>

      <SearchComponent @movieSearch="choiseMovie" />

    </header>
    
    <main>

      <CardMovie v-for="(cardN, index) in movieUserList" :key="index" :userMovie="cardN" />

    </main>
    
  </div>
</template>

<script>
import axios from 'axios';
import SearchComponent from "./components/SearchComponent.vue";
import CardMovie from "./components/CardMovie.vue";

export default {
  name: "App",
  components: {
    SearchComponent,
    CardMovie
  },
  data: function(){

    return {

      movieList: [],
      movieUserList: [],
      movieChoiseUser: "",

    };

  },
  methods: {

    choiseMovie: function(mCU){

      this.movieChoiseUser = mCU;
      
      let linkApiMovie = `https://api.themoviedb.org/3/search/movie?api_key=f80095880ece21214c44b4ace201a31c&query= + ${this.movieChoiseUser} `;

      this.movieCall(linkApiMovie);

    },

    movieCall: function(linkApiMovie){

      axios.get(linkApiMovie)
      .then((response) => {

        this.movieUserList = response.data.results;

      });

    }

  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
