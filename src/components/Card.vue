<template>
  <div class="card" v-if="cardInfo.length">
    <p v-html="cardInfo[0].question"></p>
    <div @click.once="checkAnswer($event)" id="answersList">
      <p v-for="(answer, i) in answers" :key="i" :id="`ans${i}`" v-html="answer"></p>
    </div>
    <img src="@/assets/img/replay.png" alt="Siguiente pregunta" @click="loadCard"/>
  </div>
</template>

<script>
import { ref, reactive, context, watch } from "vue";
export default {
  name: "Card",
  props: {},
  setup(props, context) {
    let cardInfo = reactive([])
    let answers = reactive([])
    let correctAnswer = ref("")
    let answer = ref(false)

    const decodeHTML = (text) => {
      let txt = document.createElement("textarea")
      txt.innerHTML = text
      return txt.value
    }

    const loadCard = () => {
      answer.value = false
      cardInfo.splice(0);
      answers.splice(0);
      fetch("https://opentdb.com/api.php?amount=1&category=9&type=multiple")
        .then((res) => res.json())
        .then((data) => {
          answers.push(...data.results[0].incorrect_answers);
          answers.splice(
            Math.round(Math.random() * 3),
            0,
            data.results[0].correct_answer
          )
          correctAnswer.value = decodeHTML(data.results[0].correct_answer)
          cardInfo.push(data.results[0])
        });
    }

    loadCard();

    const checkAnswer = (e) => {
      if (e.target.textContent != correctAnswer.value) e.target.classList.add("wrong")
      else answer.value=true
      Array.prototype.slice.call(answersList.children).forEach(ans=>{
        if(ans.textContent == correctAnswer.value) ans.classList.add("right")
      })
    }

    watch(answer,()=>{
      context.emit("answerResolved",answer)
    })

    return {
      cardInfo,
      answers,
      checkAnswer,
      loadCard
    };
  },
};
</script>

<style lang="scss" scoped>
.right {
  background-color: green;
}
.wrong {
  background-color: red;
}
</style>