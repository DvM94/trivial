<template>
  <div class="home center">
    <img alt="Logo" src="/img/logo.png">
    <router-link to="/game"><img alt="Play" src="/img/play.png" class="button" @mouseover="hover($event,'/img/play2.png')" @mouseout="hover($event,'/img/play.png')"></router-link>
  </div>
</template>

<script>
export default {
  name: 'Home',
  components: {
  },
  setup(){

    const hover = (e,link) => e.target.src = link
    
    return{
      hover
    }
  }
}
</script>

<style lang="scss" scoped>
  .home{
    width: 80%;
    max-width: 500px;
  }

  @media (max-width: 600px) {
    .button {
    width: 50%;
    max-width: 131px;
    }
  }
</style>