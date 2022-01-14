<template>
  <div id="app">

    <header>

      <SearchComponent @movieSearch="choiseMovie" />

    </header>
    
    <main>


      <span class="macro">Film:</span>
      <div class="film">
        
        <CardMovie v-for="cardN in movieUserList" :key="cardN.id" :details="cardN" />
      
      </div>

      <span class="macro">TV Show:</span>
      <div class="show">

        <CardMovie v-for="cardS in showUserList" :key="cardS.id" :details="cardS" />
      
      </div>

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
    CardMovie,
  },
  data: function(){

    return {

      movieUserList: [],
      showUserList: [],
      movieChoiseUser: "",
      linkApi: "https://api.themoviedb.org/3/search/",
      apiKey: "?api_key=f80095880ece21214c44b4ace201a31c&query=",

    };

  },
  methods: {

    choiseMovie: function(mCU){

      this.movieChoiseUser = mCU;

      let linkApiMovie = `${this.linkApi}movie${this.apiKey} + ${this.movieChoiseUser} `;

      let linkApiShow = `${this.linkApi}tv${this.apiKey} + ${this.movieChoiseUser} `;

      this.movieCall(linkApiMovie, "movie");

      this.movieCall(linkApiShow, "tv");

    },
    movieCall: function(linkApiMovie, key){

      axios.get(linkApiMovie)
      .then((response) => {

        if(key === "movie"){

          this.movieUserList = response.data.results;

        }else{

          this.showUserList = response.data.results;

        }

      });

    },

  },

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
