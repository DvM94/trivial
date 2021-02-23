<template>
  <div v-if="!endGame" class="center">
    <Card @questionsNumber="counterQuestions" @correctAnswer="counterRightAnswer"/>
    <progress id="file" max="9" :value="progress"></progress>
  </div>
  <div v-else class="center">
    <h1>FIN DE JUEGO</h1>
    <Result :rightAnswers="rightAnswers"/>
    <img src="@/assets/img/replay.png" alt="Volver a jugar" @click="replay"/>
  </div>
</template>

<script>
import { ref} from "vue"
import Card from "@/components/Card.vue"
import Result from "@/components/Result.vue"

export default {
  name: "Game",
  components:{
    Card,
    Result
  },
  setup() {
    let progress = ref(-1);
    let rightAnswers = ref(0)
    let endGame = ref(false);

    const counterQuestions = () => {
      progress.value++
      if(progress.value==10) endGame.value=true
    }

    const counterRightAnswer = () => {
      rightAnswers.value++
    }
    
    const replay = () => {
      progress.value = -1
      rightAnswers.value = 0
      endGame.value = false
    }


    return {
      progress,
      rightAnswers,
      endGame,
      counterRightAnswer,
      counterQuestions,
      replay
    };
  }
}
</script>

<style>

</style>