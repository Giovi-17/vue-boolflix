<template>
  <div id="app">

    <header>

      <SearchComponent @movieSearch="choiseMovie" />

    </header>
    
    <main>


      <span class="macro">Film:</span>
      <div class="film">
        
        <CardMovie v-for="cardN in movieUserList" :key="cardN.id" :userMovie="cardN" />
      
      </div>

      <span class="macro">TV Show:</span>
      <div class="show">

        <CardShowTV v-for="cardS in showUserList" :key="cardS.id" :userShow="cardS" />
      
      </div>

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

*{

    margin: 0;
    padding: 0;
    box-sizing: border-box;

}

#app {

  header{

    background-color: white;
    height: 40px;
    display: flex;
    align-items: center;
    color: black;

  }

  main{

    background-color: black;
    color: white;
    height: calc( 100vh - 40px );

    .macro{

      font-size: 25px;
      font-weight: bold;
      text-transform: uppercase;

    }

    .film, .show{

      display: flex;
      overflow-x: auto;
      flex-shrink: 0;
      height: calc( 50% - 30px );

    }

  }

}
</style>
