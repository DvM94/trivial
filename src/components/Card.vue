<template>
  <div class="card" v-if="cardInfo.length">
    <div class="question">
      <p v-html="cardInfo[0].question"></p>
    </div>
    <div @click.once="checkAnswer($event)" id="answersList">
      <p v-for="(answer, i) in answers" :key="i" :id="`ans${i}`" v-html="answer"></p>
    </div>
  </div>
  <img src="/img/next.png" alt="Siguiente pregunta" @click="loadCard" @mouseover="hover($event,'/img/next2.png')" @mouseout="hover($event,'/img/next.png')"/>
</template>

<script>
import { ref, reactive } from "vue";
export default {
  name: "Card",
  emits: ["questionsNumber","correctAnswer"],
  props: {},
  setup(props, context) {
    let cardInfo = reactive([])
    let answers = reactive([])
    let correctAnswer = ref("")

    const decodeHTML = (text) => {
      let txt = document.createElement("textarea")
      txt.innerHTML = text
      return txt.value
    }

    const loadCard = () => {
      context.emit("questionsNumber")
      cardInfo.splice(0);
      answers.splice(0);
      fetch("https://opentdb.com/api.php?amount=1&category=9&type=multiple")
        .then((res) => res.json())
        .then((data) => {
          answers.push(...data.results[0].incorrect_answers);
          answers.splice(Math.round(Math.random() * 3),0,data.results[0].correct_answer)
          correctAnswer.value = decodeHTML(data.results[0].correct_answer)
          console.log(correctAnswer.value)
          cardInfo.push(data.results[0])
        });
    }

    loadCard();

    const checkAnswer = (e) => {
      if (e.target.textContent == correctAnswer.value){
        e.target.classList.add("right")
        context.emit("correctAnswer")
      } 
      else {
        e.target.classList.add("wrong")
        Array.from(answersList.children).forEach(ans=>{
          if(ans.textContent == correctAnswer.value) ans.classList.add("right")
        })
      }
    }

    const hover = (e,link) => e.target.src = link

    return {
      hover,
      cardInfo,
      answers,
      checkAnswer,
      loadCard
    };
  },
};
</script>

<style lang="scss" scoped>
.card{
  width: 100%;
  max-width: 500px;
  background-color: #bce045;
  border: 2px solid black;
  border-radius: 10px;
  padding: 10px 15px;
}
.question{
  display: flex;
  align-items: center;
  background-color: white;
  margin: 10px 0;
  padding: 4px;
  height: 80px;
  border: 2px solid black;
  border-radius: 5px;
}
.right {
background-color: green;
}
.wrong {
  background-color: red;
}

</style>