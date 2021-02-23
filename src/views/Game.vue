<template>
  <div v-if="!endGame">
    <Card @correctAnswers="counterCorrectAnswers" @countQuestions="countQuestions" />
    <progress id="file" max="10" :value="progress"></progress>
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
    let progress = ref(0);
    let correctAnswers = ref(0);
    let endGame = ref(false);

    const counterCorrectAnswers = () => {
      correctAnswers.value++
      console.log(correctAnswers.value)
    }

    const countQuestions = dato => {
      progress.value++
      if(progress.value==10) endGame.value=true
    }

    return {
      progress,
      correctAnswers,
      endGame,
      counterCorrectAnswers,
      countQuestions
    };
  }
}
</script>

<style>

</style>