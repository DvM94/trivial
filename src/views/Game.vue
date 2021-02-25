<template>
  <div v-if="!endGame" class="main center">
    <Card @questionsNumber="counterQuestions" @correctAnswer="counterRightAnswer"/>
    <progress id="file" max="9" :value="progress"></progress>
  </div>
  <div v-else class="main center">
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

<style lang="scss" scoped>

.main {
  width: 85%;
  max-width: 650px;
}

progress {
  width: 70%;
  height: 30px;
  border-radius: 10px;
  padding: 5px 10px;
}
progress::-webkit-progress-bar {
  height: 35px;
  background-color: rgb(179, 177, 177);
  box-shadow: 3px 3px 5px gray;
  border-radius: 10px;
  border: 1px solid black;
  padding: 7px 15px;
}
progress::-webkit-progress-value {
  background-color: #4b72a6;
  border: 1px solid black;
  border-radius: 5px 0 0 5px;
}

@media (max-width: 600px) {

  progress {
  width: 80%;
  }
}

</style>
