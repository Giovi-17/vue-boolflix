<template>

  <div>

    <label for="">Cerca un film o una serie tv:</label>
    <input v-model="movieSearchUser" type="text">
    <button @click= "$emit('movieSearch', movieSearchUser)" >Cerca</button>

  </div>
    
</template>

<script>
export default {
  name: "SearchComponent",
  data: function(){

    return {

      movieSearchUser: [],

    }

  }
};
</script>

<style lang="scss" scoped>

</style>