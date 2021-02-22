<template>
  <div v-if="!endGame">
    <Card @answerResolved="checkAnswer"/>
    <progress id="file" max="9" :value="progress"></progress>
  </div>
  <div v-else>
    <h1>FIN DE JUEGO</h1>
  </div>
</template>

<script>
import { ref, reactive } from "vue"
import Card from "@/components/Card.vue"

export default {
  name: "Game",
  components:{
    Card
  },
  setup() {
    let progress = ref(-1);
    let counter = ref(0)
    let endGame = ref(false);

    function checkAnswer(dato){
      if(dato.value==true) counter.value++
      console.log(counter.value)
    }

    const checkProgress = () => {
      if(progress.value==9)
        endGame.value=true
    }

    return {
      progress,
      counter,
      endGame,
      checkAnswer
    };
  }
}
</script>

<style>

</style>