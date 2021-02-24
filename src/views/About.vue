<template>
  <div class="about">
    <h1>This is an about page</h1>
    <img alt="Nuria" src="/img/nuria.png" class="logo">
    <img alt="Dani" src="/img/dani.png" class="logo">
    <router-link to="/game"><img alt="Vue logo" src="/img/play.png" @mouseover="hover($event,'/img/play2.png')" @mouseout="hover($event,'/img/play.png')"></router-link>
  </div>
</template>

<script>

export default {
  name: 'About',
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
.logo{
  width: 30%;
  max-width: 350px;
}
</style>