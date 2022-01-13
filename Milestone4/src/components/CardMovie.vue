<template>

<ul @mouseleave="showCard = true">
  
  <li @mouseenter="showCard = false" v-show="showCard" class="movieImg"><img :src="imageMovie(mImg)" alt=""></li>
  <li v-show="!showCard">Titolo: {{ userMovie.title }}</li>
  <li v-show="!showCard">Titolo Originale: {{ userMovie.original_title }}</li>
  <li v-show="!showCard" class="imgFlag">Lingua: <img :src="flagC(flag)" :alt="userMovie.original_language"></li>
  <li v-show="!showCard">Voto: <i v-for="( star, index ) in averageStar()" :key="index" class="fas fa-star"></i><i v-for="( starE, index ) in emptyStar()" :key="index" class="far fa-star"></i></li>
  <li v-show="!showCard">Descrizione: {{ userMovie.overview }}</li>

</ul>
    
</template>

<script>
export default {
  name: "CardMovie",
  props: {
    userMovie: Object,
  },
  data: function(){

    return {

      showCard: true

    }

  },
  methods: {

    flagC: function(flag){

      if(this.userMovie.original_language === "it"){

        flag = "https://upload.wikimedia.org/wikipedia/commons/thumb/c/ca/Bandiera_italiana_foto.svg/2560px-Bandiera_italiana_foto.svg.png";

      }
      else if(this.userMovie.original_language === "en"){

        flag = "https://upload.wikimedia.org/wikipedia/commons/thumb/e/e2/Flag_of_the_United_States_%28Pantone%29.svg/280px-Flag_of_the_United_States_%28Pantone%29.svg.png";
      
      }

      return flag;

    },

    imageMovie: function(mImg){

      mImg = `http://image.tmdb.org/t/p/w342${this.userMovie.poster_path}`;

      return mImg;

    },

    averageStar: function(){

      let star = this.userMovie.vote_average;

      let cStar = Math.round( star, 1 );

      cStar = cStar / 2;

      return cStar;

    },

    emptyStar: function(){

      let star = this.userMovie.vote_average;

      let cStar = Math.round( star, 1 );

      cStar = cStar / 2;

      let eStar= 5 - cStar;

      return eStar;

    },

  }
};
</script>

<style lang="scss" scoped>

ul{

  list-style-type: none;
  margin: 15px;
  display: flex;
  width: 343px;
  flex-direction: column;
  cursor: pointer;
  overflow-y: auto;
  flex-shrink: 0;

  li{

    width: 342px;
    margin: 5px 0;
    font-size: 20px;

  }

  .imgFlag img{

    width: 20px;

  }

}

</style>
