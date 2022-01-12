<template>
  <div id="app">

    <header>

      <SearchComponent @movieSearch="choiseMovie" />

    </header>
    
    <main>

      Film:
      <CardMovie v-for="(cardN, index) in movieUserList" :key="index" :userMovie="cardN" />

      <br>

      TV Show:
      <CardShowTV v-for="(cardS, index) in showUserList" :key="index" :userShow="cardS" />

    </main>
    
  </div>
</template>

<script>
import axios from 'axios';
import SearchComponent from "./components/SearchComponent.vue";
import CardMovie from "./components/CardMovie.vue";
import CardShowTV from "./components/CardShowTV.vue";


export default {
  name: "App",
  components: {
    SearchComponent,
    CardMovie,
    CardShowTV
  },
  data: function(){

    return {

      movieUserList: [],
      showUserList: [],
      movieChoiseUser: "",
      showChoiseUser: "",

    };

  },
  methods: {

    choiseMovie: function(mCU){

      this.movieChoiseUser = mCU;

      this.showChoiseUser = mCU;

      let linkApiMovie = `https://api.themoviedb.org/3/search/movie?api_key=f80095880ece21214c44b4ace201a31c&query= + ${this.movieChoiseUser} `;

      let linkApiShow = `https://api.themoviedb.org/3/search/tv?api_key=f80095880ece21214c44b4ace201a31c&query= + ${this.movieChoiseUser} `;

      this.movieCall(linkApiMovie);

      this.showCall(linkApiShow);

    },

    movieCall: function(linkApiMovie){

      axios.get(linkApiMovie)
      .then((response) => {

        this.movieUserList = response.data.results;

      });

    },

    showCall: function(linkApiShow){

      axios.get(linkApiShow)
      .then((response) => {

        this.showUserList = response.data.results;

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
