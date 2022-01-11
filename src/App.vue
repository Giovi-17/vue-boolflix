<template>
  <div id="app">
    
    <main>

      <SearchComponent @movieSearch="choiseMovie" />

    </main>
    
  </div>
</template>

<script>
import axios from 'axios';
import SearchComponent from "./components/SearchComponent.vue";

export default {
  name: "App",
  components: {
    SearchComponent,
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
      
      let linkApiMovie = `https://api.themoviedb.org/3/search/tv?api_key=f80095880ece21214c44b4ace201a31c&query= + ${this.movieChoiseUser} `;

      console.log(linkApiMovie);

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
