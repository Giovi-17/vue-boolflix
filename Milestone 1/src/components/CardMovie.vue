<template>

<ul>

    <li>Titolo: {{ userMovie.title }}</li>
    <li>Titolo Originale: {{ userMovie.original_title }}</li>
    <li>Lingua: {{ userMovie.original_language }}</li>
    <li>Voto: {{ userMovie.vote_average }}</li>

</ul>
    
</template>

<script>
export default {
  name: "CardMovie",
  props: {
    userMovie: Object,
  },
};
</script>

<style lang="scss" scoped>

ul{

    list-style-type: none;
    border: 1px solid black;
    margin: 15px;

}

</style>
