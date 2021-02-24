<template>
  <div class="home">
    <img alt="Vue logo" src="/img/logo.png">
    <router-link to="/game"><img alt="Vue logo" src="/img/play.png" @mouseover="hover($event,'/img/play2.png')" @mouseout="hover($event,'/img/play.png')"></router-link>
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
