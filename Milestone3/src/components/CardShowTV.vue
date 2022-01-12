<template>

<ul>

    <li class="showImg"><img :src="imageShow(sImg)" alt=""></li>
    <li>Titolo: {{ userShow.name }}</li>
    <li>Titolo Originale: {{ userShow.original_name }}</li>
    <li class="imgFlag">Lingua: <img :src="flagC(flag)" :alt="userShow.original_language"></li>
    <li>Voto: {{ userShow.vote_average }}</li>

</ul>
    
</template>

<script>
export default {
  name: "CardShowTV",
  props: {
    userShow: Object,
  },
  methods: {

    flagC: function(flag){

      if(this.userShow.original_language === "it"){

        flag = "https://upload.wikimedia.org/wikipedia/commons/thumb/c/ca/Bandiera_italiana_foto.svg/2560px-Bandiera_italiana_foto.svg.png";

      }
      else if(this.userShow.original_language === "en"){

        flag = "https://upload.wikimedia.org/wikipedia/commons/thumb/e/e2/Flag_of_the_United_States_%28Pantone%29.svg/280px-Flag_of_the_United_States_%28Pantone%29.svg.png";
      
      }

      return flag;

    },

    imageShow: function(sImg){

      sImg = `http://image.tmdb.org/t/p/w500${this.userShow.poster_path}`;

      return sImg;

    }

  }
};
</script>

<style lang="scss" scoped>

ul{

    list-style-type: none;
    border: 1px solid black;
    margin: 15px;

    .showImg img{

      width: 100px;

    }

    .imgFlag img{

      width: 20px;

    }

}

</style>
