<template>

<ul @mouseleave="showCard = true">
  
  <li @mouseenter="showCard = false" v-show="showCard" class="movieImg"><img :src="imageMovie(mImg)" alt=""></li>
  <li v-show="!showCard">Titolo: {{ details.title || details.name }}</li>
  <li v-show="!showCard">Titolo Originale: {{ details.original_title  || details.original_name }}</li>
  <li v-show="!showCard" class="imgFlag">Lingua: <img :src="flagC(flag)" :alt="details.original_language"></li>
  <li v-show="!showCard">Voto: <i v-for="( star, index ) in averageStar()" :key="index" class="fas fa-star"></i><i v-for="( starE, index ) in emptyStar()" :key="index" class="far fa-star"></i></li>
  <li v-show="!showCard">Descrizione: {{ details.overview }}</li>

</ul>
    
</template>

<script>
export default {
  name: "CardMovie",
  props: {
    details: Object,
  },
  data: function(){

    return {

      showCard: true,
      posterImg : "http://image.tmdb.org/t/p/w342"

    }

  },
  methods: {

    flagC: function(flag){

      if(this.details.original_language === "it"){

        flag = "https://upload.wikimedia.org/wikipedia/commons/thumb/c/ca/Bandiera_italiana_foto.svg/2560px-Bandiera_italiana_foto.svg.png";

      }
      else if(this.details.original_language === "en"){

        flag = "https://upload.wikimedia.org/wikipedia/commons/thumb/e/e2/Flag_of_the_United_States_%28Pantone%29.svg/280px-Flag_of_the_United_States_%28Pantone%29.svg.png";
      
      }

      return flag;

    },

    imageMovie: function(mImg){

      mImg = `${this.posterImg}${this.details.poster_path}`;

      if(!this.details.poster_path){

        mImg = "https://eu.community.samsung.com/t5/image/serverpage/image-id/149270i0E361FEBA84DA302/image-size/large?v=v2&px=999" ;

      }
      
      return mImg;

    },

    averageStar: function(){

      let star = this.details.vote_average;

      let cStar = Math.round( star, 1 );

      cStar = cStar / 2;

      return cStar;

    },

    emptyStar: function(){

      let cStar =  this.averageStar();

      let eStar = 5 - cStar;

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

  .movieImg img{

    max-width: 342px;

  }

  .imgFlag img{

    width: 20px;

  }

}

</style>
