<template>

<ul>

    <li>Titolo: {{ userMovie.title }}</li>
    <li>Titolo Originale: {{ userMovie.original_title }}</li>
    <li class="imgFlag">Lingua: <img :src="flagC(flag)" :alt="userMovie.original_language"></li>
    <li>Voto: {{ userMovie.vote_average }}</li>

</ul>
    
</template>

<script>
export default {
  name: "CardMovie",
  props: {
    userMovie: Object,
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

    }

  }
};
</script>

<style lang="scss" scoped>

ul{

    list-style-type: none;
    border: 1px solid black;
    margin: 15px;

    .imgFlag img{

      width: 20px;

    }

}

</style>
