<template>
  <div id="nav">
    <router-link to="/"><img alt="Home" src="@/assets/img/home.png"></router-link>
    <router-link to="/about"><img alt="About" src="@/assets/img/about.png"></router-link>
  </div>
  <router-view/>
</template>

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
  background-image: url("./assets/img/background.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  height: 100vh;
}
img{
  max-width: 100%;
}
#nav {
  position: fixed;
  width: 100%;
  max-width: 1200px;
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
