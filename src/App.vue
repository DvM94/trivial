<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link> |
    <router-link to="/game">Game</router-link>
  </div>
  <router-view/>
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Indie+Flower&display=swap');

#app {
  font-family: 'Acme', Arial, sans-serif;
  text-align: center;
}

#nav {
  padding: 30px;

}
</style>
