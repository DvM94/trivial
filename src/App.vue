<template>
  <div id="nav">
    <router-link to="/"><img alt="Home" src=/img/home.png @mouseover="hover($event,'/img/home2.png')" @mouseout="hover($event,'/img/home.png')"></router-link>
    <router-link to="/about"><img alt="About" src="/img/about.png" @mouseover="hover($event,'/img/about2.png')" @mouseout="hover($event,'/img/about.png')"></router-link>
  </div>
  <router-view/>
</template>

<script>
export default {
  setup(){

    const hover = (e,link) => e.target.src = link

    return{
      hover
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Indie+Flower&display=swap');

* {
  font-family: 'Acme', Arial, sans-serif;
  text-align: center;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body{
  background-image: url("/img/background.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  height: 100vh;
}
img{
  max-width: 100%;
}
#nav {
  position: fixed;
  z-index: 10;
  width: 100%;
  max-width: 1000px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  justify-content: space-between;
  padding: 30px;
}
.center{
  transform: translate(-50%,-50%);
  position: absolute;
  top: 50%;
  left: 50%;
}

</style>
